---
title: "Why Your Docker Images Are So Big (And How to Fix It)"
pubDate: "2025-10-10"
description: "Learn why Docker images become bloated and discover practical techniques to reduce image size by 80% or more. Includes real-world examples and best practices."
tags: ["docker", "optimization", "devops", "containers", "performance"]
image: "/images/docker-images-are-too-big.png"
readTime: "12 min read"
---

# Why Your Docker Images Are So Big (And How to Fix It)

Ever wondered why your Docker images are taking forever to build and deploy? You're not alone. Bloated Docker images are one of the most common problems in containerized applications. 

In large scale CI/CD pipelines, bloated images can waste hours of compute time and gigabytes of storage per build. Let's fix this once and for all.

## The Problem: Bloated Images

### Common Culprits
- **Large base images** 
- **Unnecessary packages** and dependencies
- **Build artifacts** left in final image
- **Multiple layers** with redundant data
- **No cleanup** after package installation

### Real-World Impact
- **Slower deployments** (5-10x longer)
- **Higher storage costs** (10x more space)
- **Network bottlenecks** (longer downloads)
- **Security risks** (more attack surface)

## Before and After: A Real Example

For the example below, I used an app.py file that demonstrates a real Flask web application with dependencies.

Step 1: Create a folder
```
mkdir docker-tests
```

Step 2: In the folder, create an app.py file.

[app.py]
```python
from flask import Flask, jsonify
import requests
import json
from datetime import datetime

app = Flask(__name__)

@app.route('/')
def home():
    return jsonify({
        "message": "Hello from Docker!",
        "timestamp": datetime.now().isoformat(),
        "status": "running"
    })

@app.route('/health')
def health():
    return jsonify({"status": "healthy"})

@app.route('/external')
def external():
    try:
        response = requests.get('https://httpbin.org/json', timeout=5)
        return jsonify({
            "external_data": response.json(),
            "status": "success"
        })
    except Exception as e:
        return jsonify({"error": str(e), "status": "failed"}), 500

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=False)
```


Step 3. Create a requirements.txt file
```
flask==2.3.3
requests==2.31.0
numpy==1.24.3
pandas==2.0.3
```
Note: NumPy and Pandas are installed for demonstration purposes only and aren’t used in app.py.

---
### The Bloated Version

Step 4: Create a dockerfile

Dockerfile.bloated
```dockerfile
# ❌ BAD: Bloated image (931MB)
FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install -y python3 python3-pip
RUN pip3 install flask requests numpy pandas
COPY . /app
WORKDIR /app
EXPOSE 5000
CMD ["python3", "app.py"]
```

Step 5: Build the Image
```
docker build -t ubuntu-bloated -f Dockerfile.bloated .
```

---

### The Optimized Version of Ubuntu

Step 6: Create a dockerfile

Dockerfile.optimized
```dockerfile
FROM ubuntu:20.04 AS builder
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
COPY requirements.txt .
RUN pip3 install --no-cache-dir --user -r requirements.txt

FROM ubuntu:20.04
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    useradd -m appuser
COPY --from=builder /root/.local /home/appuser/.local
COPY . /app
WORKDIR /app
RUN chown -R appuser:appuser /app
USER appuser
EXPOSE 5000
CMD ["python3", "app.py"]
```


Step 7: Build the Image
```
docker build -t ubuntu-optimized -f Dockerfile.optimized .
```

---

### The Slim Build

Step 8: Create a dockerfile

Dockerfile.slim
```dockerfile
FROM python:3.9-slim AS builder
COPY requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt

FROM python:3.9-slim
COPY --from=builder /root/.local /root/.local
COPY . /app
WORKDIR /app
RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser
EXPOSE 5000
CMD ["python", "app.py"]
```

Step 9: Build the Image
```
docker build -t slim-optimized -f Dockerfile.slim .
```
---
### The Alpine Build (with compatibility issues)

Step 10: Create the docker file

Dockerfile.alpine
```dockerfile
# Alpine - smallest but compatibility issues
FROM python:3.9-alpine
COPY requirements.txt .
RUN apk add --no-cache --virtual .build-deps gcc musl-dev && \
    pip install --no-cache-dir -r requirements.txt && \
    apk del .build-deps
COPY . /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

Step 11: Build the Image
```
docker build -t alpine-optimized -f Dockerfile.alpine .
```
---

## Results

Lets first look at the base imaaages and then current image sizes.

#### Base images
```bash
docker pull ubuntu:20.04
docker images ubuntu:20.04
# Size: ~109MB

docker pull python:3.9-slim
docker images python:3.9-slim
# Size: ~194MB

docker pull python:3.9-alpine
docker images python:3.9-alpine
# Size: ~79.7MB
```

#### Build Image sizes
Get the sizes
```bash
docker images | grep -E "(ubuntu-bloated|slim-optimized|ubuntu-optimized|alpine-optimized)"
```
Image sizes
```bash
ubuntu-bloated     latest    99cfce6b34ff   14 minutes ago       931MB
ubuntu-optimized   latest    186773c0ac9a   19 minutes ago       168MB
alpine-optimized   latest    b13738bb780d   About a minute ago   101MB
slim-optimized     latest    cbcd80d00465   13 minutes ago       215MB
```

Interesting.. Alpine appears the smallest from this output, and Ubuntu optimized is the next smallest. Let's explore more. Let's look at the base images before we optimize.


Did alpine win? Not exactly. For size, yes, for functionality, no. 

Alpine is to be used with caution
- Smallest final image (101MB).
- Uses musl libc instead of glibc → can break some Python packages (DNS quirks, memory allocation issues, some C extensions).
- Alpine works best for statically compiled languages, dynamic languages with C extensions (Python, Ruby) can run into subtle runtime issues.
- Fine if you know your dependencies work cleanly with musl, but more fragile in production.

**So is it ubuntu optimized or slim as the winner?**

Why choose Ubuntu-optimized over Slim?
- Its not as clear cut as you would hope, it "depends". 
- Let's see why Slim exists and why Ubuntu beats slim in our example.

Why slim exists
- Slim images are stripped-down Python images with fewer extra packages and libraries.
- Intended to reduce image size compared to the full python:X.X image.
- Great if you know exactly what dependencies you need and can install them without adding too many extras.

Why Ubuntu-optimized beats slim in ourr example
- You almost always need system libraries, compilers, or dev tools for Python packages like numpy, pandas, or anything with C extensions.
- Installing those on slim adds layers and increases size.
- In some Python apps with C extension dependencies, Ubuntu optimized can be smaller than Python slim due to required build dependencies.
- Do not pick slim just because it “sounds smaller”. For Python, Ubuntu-optimized can often be smaller, as safe, and easier to maintain.
- Slim can still be useful for simple Python apps with pure Python dependencies, but for most production apps, Ubuntu wins.

When to pick Slim over ubuntu?
- Pick Ubuntu-optimized for Python unless you have a strict requirement for the absolute smallest image and have tested all dependencies on slim.
- Slim is better for experienced teams who can manage missing libraries and want slightly smaller builds (sometimes smaller than Ubuntu in very minimal cases).

#### The winner? 
- For our example, **Ubuntu-optimized.** 

---

## Python Base Image Decision Matrix

| Image | Size (with dependencies) | Compatibility | Security | Debugging | Use Case | Overall Rating | Reason |
|-------|------|---------------|----------|-----------|----------|----------------|---------|
| Ubuntu | 900MB+  | Excellent | Poor | Easy | Development | ⭐⭐ (Easiest) | Too large for production |
| Ubuntu Optimized | ~168MB | Excellent | Good | Easy | **Production** | ⭐⭐⭐⭐⭐ (Best overall) | Best balance of compatibility, debugging, stability |
| Alpine Optimized | ~101MB | Poor | Good | Hard | Simple apps only | ⭐⭐ (Size over compatibility) | Compatibility issues with C extensions |
| Python Slim Optimized| ~215MB | Excellent | Good | Easy | **Production** | ⭐⭐⭐⭐ (Good alternative) | Good for pure Python apps |
| distroless/python3 Optimized  | ~93.8MB | Good* | Excellent | Hard | Security-critical | ⭐⭐⭐⭐ (Security-focused) | Excellent security, limited flexibility |

*Supports only pre-installed Python runtime and pure Python dependencies; installing additional packages is difficult.


### **Recommendation for python applications:** 
- Use ubuntu:20.04 optimized for Python apps with C-extension dependencies.
- **Pros:**
    - Excellent compatibility with Python packages like numpy, pandas, and scipy
    - Easier debugging with full shell and package manager access
    - Predictable and stable build environment for production
- **Cons:**
    - Larger attack surface compared to slim or distroless images
    - Requires installing Python and dependencies manually

### Close Runner-Up: python:3.9-slim
- **Pros:** Minimal attack surface, small size, no shell/package manager
- **Cons:** Hard to debug, no shell access, limited to pure Python apps

### Close Runner-Up: python:3.9-slim
- **Pros:** Minimal attack surface, small size, no shell/package manager
- **Cons:** Hard to debug, no shell access, limited to pure Python apps


### Takeaway

For Python applications that rely on system libraries or heavy C-extension packages like numpy, pandas, or scipy, Ubuntu-optimized is often the better choice. It provides a stable, predictable environment with full shell access, easier debugging, and the flexibility to install exactly what your application needs. In many cases, the final image size can even be smaller than Python slim, because you avoid pulling in extra build dependencies that slim requires for C extensions.

That said, Python slim remains a strong alternative for applications that are mostly pure Python. It offers a minimal attack surface, a smaller base, and fewer moving parts, making it ideal for lightweight apps where full system libraries aren’t needed. Choosing slim is especially valuable when security and minimal runtime footprint are top priorities, or when you want to enforce a strict “pure Python only” environment.

**Rule of Thumb:**
- Ubuntu-optimized: Use for complex Python apps with compiled dependencies.
- Python slim: Use for lightweight, pure-Python apps where minimal attack surface and small image size matter most.



## 7 Techniques to Shrink Your Images

### 1. Choose the Right Base Image

Why it matters: Choosing a smaller base image helps reduce your image size, attack surface, and build time. However, make sure the image is compatible with your use case, and consider its installation dependencies, sometimes a slightly larger image may be more optimal depending on the libraries and tools your application needs.

Looking at just raw base images:

**Large Base Images:**
```dockerfile
FROM ubuntu:20.04  # 72MB
FROM node:16        # 900MB
FROM python:3.9    # 900MB
```

**Alternatives:**
```dockerfile
FROM alpine:3.15    # 5MB
FROM node:16-alpine # 120MB
FROM python:3.9-slim # ~194MB (better Python compatibility)
```

The best approach is to test which images successfully build, ensure all dependencies work, and choose one that minimizes both image bloat and attack surface.

** Python + Alpine Warning:**
While Alpine images are smaller, they use musl libc instead of glibc, which can cause compatibility issues with Python packages containing C extensions. Many popular packages (numpy, pandas, scipy, etc.) may fail to install or run properly.


### 2. Multi-Stage Builds

Why it matters: Multi-stage builds let you separate build-time dependencies (compilers, dev tools) from runtime dependencies, drastically reducing image size and attack surface. I can also use distroless while using multi-stage builds.

**Single stage build**
```dockerfile
# Single-stage build
FROM ubuntu:20.04
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt
COPY . /app
WORKDIR /app
RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser
EXPOSE 5000
CMD ["python3", "app.py"]
```

**Multi-stage**
```dockerfile
FROM ubuntu:20.04 AS builder
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip gcc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
COPY requirements.txt .
RUN pip3 install --no-cache-dir --user -r requirements.txt

# Production stage - Distroless for minimal attack surface
FROM gcr.io/distroless/python3
COPY --from=builder /root/.local /root/.local
COPY . /app
WORKDIR /app
CMD ["app.py"]
```

### What Changed and Why

**Before (Single stage):** All dependencies installed in one stage, including build tools and package managers that aren't needed at runtime.

**After (Multi-stage):** 
- **Build stage:** Installs Python, pip, and all dependencies
- **Production stage:** Only installs Python runtime and copies the built dependencies
- **Result:** Smaller final image with no build tools or package managers

**Key Benefits:**
- **Security:** No build tools in final image
- **Size:** Removes unnecessary build dependencies
- **Maintenance:** Cleaner separation of concerns
- **Debugging:** Easier to troubleshoot build vs runtime issues


### 3. Combine RUN Commands

Why it matters: Combining RUN commands matters because it prevents temporary files from being saved in separate Docker layers, keeping the final image smaller and cleaner.

**❌ Bad:**
```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y wget
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
```

**✅ Good:**
```dockerfile
RUN apt-get update && \
    apt-get install -y curl wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
```

### 4. Use .dockerignore

Why it matters: It prevents unnecessary files from being included in the build context, reducing image size and speeding up builds.

Example of .dockerignore for a project
```dockerignore
node_modules
npm-debug.log
.git
.gitignore
README.md
.env
.nyc_output
coverage
.nyc_output
.vscode
```

### 5. Remove Package Managers

Why it matters: Package managers like `apt`, `apk`, and `pip` are great for building, but leaving them in your final image increases size and attack surface.

```dockerfile
# Install dependencies during build
RUN apk add --no-cache python3 py3-pip

# Remove package manager in the final stage only
RUN apk del py3-pip
```

### 6. Copy Only What You Need

Why it matters: It keeps the image smaller, avoids including sensitive or unnecessary files, and improves Docker layer caching efficiency for faster builds.

```dockerfile
# Copy only necessary files
COPY package.json package-lock.json ./
RUN npm ci --only=production
COPY src/ ./src/
```

### 7. Use Distroless Images

Why it matters:  Distroless images contain only your application and its runtime dependencies. Meaning no package manager, shell, or OS libraries. That results in a smaller size and fewer vulnerabilities. 

```dockerfile
# Build stage - MUST use a full image with build tools
FROM ubuntu:20.04 AS builder
RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip gcc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
COPY requirements.txt .
RUN pip3 install --no-cache-dir --user -r requirements.txt

# Production stage - Distroless for minimal attack surface
FROM gcr.io/distroless/python3
COPY --from=builder /root/.local /root/.local
COPY . /app
WORKDIR /app
CMD ["app.py"]
```

Note: Distroless images cannot be used in build stages because they contain no package managers, shells, or build tools, only the minimal runtime needed to execute your application. You must use a full base image (like Ubuntu or Python slim) in the build stage to install dependencies, then copy the built application to a distroless runtime image for maximum security.

## Advanced Optimization Techniques

### Layer Caching Optimization

Why it matters: Copy only dependency files first (requirements.txt) to maximize Docker cache efficiency.

```dockerfile
# Order matters for caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
```

### Enable BuildKit for Faster Builds

Why it matters: You can enable BuildKit to get better caching, parallel builds, and smaller final layers.

You don’t need to modify the Dockerfile; just build with:
```dockerfile
DOCKER_BUILDKIT=1 docker build -t your-app .
```

### Build Arguments for Conditional Installs

Why it matters: Allows optional installation of dev tools without bloating the production image.

```dockerfile
ARG INSTALL_DEV_TOOLS=false
RUN if [ "$INSTALL_DEV_TOOLS" = "true" ]; then \
        apt-get install -y gcc g++ make vim git; \
    fi
```

### Health Checks

Why it matters: Health checks help orchestration tools (like Kubernetes/ECS) automatically restart unhealthy containers.

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD python -c "import requests; requests.get('http://localhost:5000/health')" || exit 1
```

## Tools to Analyze Your Images

### 1. Docker History

This command shows all the layers in a Docker image, including the commands that created them and their sizes. This helps identify which layers are largest and where you can optimize your Dockerfile.

```bash
docker history your-image:latest
```

### 2. Dive Tool

The Dive tool lets you inspect a Docker image layer by layer, showing the files added in each layer and their sizes. It also helps identify ways to reduce image size and improve build efficiency.

```bash
# Install dive (see current releases here: https://github.com/wagoodman/dive/releases/)
# Dive is "A tool for exploring a Docker image, layer contents, and discovering ways to shrink the size of your Docker/OCI image."
curl -LO https://github.com/wagoodman/dive/releases/download/v0.10.0/dive_0.10.0_linux_amd64.deb
sudo dpkg -i dive_0.10.0_linux_amd64.deb

# Analyze image
dive your-image:latest
```

### 3. Docker Slim

Analyzes your image and automatically creates a smaller optimized version by removing unnecessary files and dependencies. It helps reduce image size and attack surface while keeping the app functional.

```bash
docker run -it --rm \
  -v /var/run/docker.sock:/var/run/docker.sock \
  dslim/docker-slim build your-image:latest

#-it runs interactively so you can see the output.
#--rm removes the container after it finishes.
#-v /var/run/docker.sock:/var/run/docker.sock gives Docker Slim access to your Docker daemon so it can inspect and build images.
#dslim/docker-slim build your-image:latest tells it to optimize your-image:latest.
```

## Best Practices Checklist

- [ ] Use the right image for the job
- [ ] Implement multi-stage builds
- [ ] Combine RUN commands
- [ ] Use .dockerignore file
- [ ] Remove package managers after install
- [ ] Copy only necessary files
- [ ] Use specific version tags
- [ ] Regular security scanning

## Common Mistakes to Avoid

1. Installing unnecessary packages
2. Not cleaning up package cache
3. Copying entire project directories
4. Using latest tags in production
5. Not using multi-stage builds
6. Ignoring .dockerignore

## Testing Your Optimizations

### Size Comparison
```bash
# Before
docker images | grep your-app
# your-app    latest    2.1GB

# After
docker images | grep your-app
# your-app    latest    45MB
```

### Build Time Comparison
```bash
time docker build -t your-app .
# Before: 8m 23s
# After:  2m 15s
```

## **AREAS TO TEST/ADD:**

1. **Test with your actual application** - Replace the example with your real app
2. **Add security scanning** - Run `docker scan your-image` after optimization
3. **Performance testing** - Measure startup time before/after
4. **Add monitoring** - Track image size over time
5. **Document your process** - Create a checklist for your team

## Next Steps

1. **Audit your current images** using `dive`
2. **Start with base image optimization**
3. **Implement multi-stage builds**
4. **Set up automated scanning**
5. **Monitor improvements over time**

Remember: The goal isn’t just smaller images… it’s faster deployments, tighter security, and developers who don’t need to docker prune their sanity. Start with one technique and build from there.

## Additional Resources

- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)
- [Alpine Linux Packages](https://pkgs.alpinelinux.org/packages)
- [Distroless Images](https://github.com/GoogleContainerTools/distroless)
- [Dive Tool Documentation](https://github.com/wagoodman/dive)
