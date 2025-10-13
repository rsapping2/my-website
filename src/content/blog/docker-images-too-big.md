---
title: "Why Your Docker Images Are So Big (And How to Fix It)"
pubDate: "2025-10-10"
description: "Learn why Docker images become bloated and discover practical techniques to reduce image size by 80% or more. Includes real-world examples and best practices."
tags: ["docker", "optimization", "devops", "containers", "performance"]
image: "/images/docker-images-are-too-big.png"
---

# Why Your Docker Images Are So Big (And How to Fix It)

Ever wondered why your Docker images are taking forever to build and deploy? You're not alone. Bloated Docker images are one of the most common problems in containerized applications. 

In large scale CI/CD pipelines, bloated images can waste hours of compute time and gigabytes of storage per build. Let's fix this once and for all.

## The Problem: Bloated Images

### Common Culprits
- **Large base images** (Ubuntu: 72MB → Alpine: 5MB)
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

For the example below, I used an app.py file, which is just a print statement.

```python
print("Hello world")
```

### The Bloated Version

Create a folder
```
mkdir docker-bloated
```
Add the app.py file to it.

Create a dockerfile
```dockerfile
# ❌ BAD: Bloated image (2.1GB)
FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install -y python3 python3-pip
RUN pip3 install flask requests numpy pandas
COPY . /app
WORKDIR /app
RUN python3 app.py
```

Test the build
```
docker build -t test-bloated .
```

### The Optimized Version

Create a folder
```
mkdir docker-optimized
```
Add the app.py file to it.

Create a dockerfile
```dockerfile
# ✅ GOOD: Optimized image (45MB)
FROM python:3.9-alpine
RUN apk add --no-cache --virtual .build-deps gcc musl-dev
RUN pip install --no-cache-dir flask requests
RUN apk del .build-deps
COPY . /app
WORKDIR /app
CMD ["python", "app.py"]
```

Test the build
```
docker build -t test-optimized .
```

### Compare Sizes
```bash
docker images | grep test- 
```
Results
```bash
test-optimized     latest    b42aa86a2ad4   About a minute ago   338MB
test-bloated       latest    c1d0bd88f0ab   9 minutes ago        931MB
```

**Result: At least 63.7% size reduction!**

You can also compare the intial base images, which is still about a 29.5% reduction.

```bash
docker pull ubuntu:20.04
docker images ubuntu:20.04
# Size: ~109MB

docker pull python:3.9-alpine
docker images python:3.9-alpine
# Size: ~76.8MB
```

## 7 Techniques to Shrink Your Images

### 1. Choose the Right Base Image

Why it matters: Choosing a smaller base image matters because it reduces your image size, attack surface, and build time.

**❌ Avoid:**
```dockerfile
FROM ubuntu:20.04  # 72MB
FROM node:16        # 900MB
FROM python:3.9    # 900MB
```

**✅ Use:**
```dockerfile
FROM alpine:3.15    # 5MB
FROM node:16-alpine # 120MB
FROM python:3.9-alpine # 45MB
```

### 2. Multi-Stage Builds

Why it matterrs: Multi-stage builds let you separate build-time dependencies (compilers, dev tools) from runtime dependencies, drastically reducing image size and attack surface. 

```dockerfile

# Build stage
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Production stage
FROM node:16-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

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

Why it mattters: It keeps the image smaller, avoids including sensitive or unnecessary files, and improves Docker layer caching efficiency for faster builds.

```dockerfile
# Copy only necessary files
COPY package.json package-lock.json ./
RUN npm ci --only=production
COPY src/ ./src/
```

### 7. Use Distroless Images

Why it matters:  Distroless images contain only your application and its runtime dependencies. Meaning no package manager, shell, or OS libraries. That results in a smaller size and fewer vulnerabilities. 

```dockerfile
# For Go applications
FROM gcr.io/distroless/base-debian10
COPY app /app
CMD ["/app"]
```

## Advanced Optimization Techniques

### Layer Caching Optimization

Why it matters: Copy only dependency files first (package.json/package-lock.json) to maximize Docker cache efficiency.

```dockerfile
# Order matters for caching
COPY package.json package-lock.json ./
RUN npm ci --only=production
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
        apt-get install -y vim git; \
    fi
```

### Health Checks

Why it matters: Health checks help orchestration tools (like Kubernetes/ECS) automatically restart unhealthy containers.

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:3000/health || exit 1
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

- [ ] Use Alpine or distroless base images
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

## 🚀 **AREAS TO TEST/ADD:**

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
