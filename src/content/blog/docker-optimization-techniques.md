---
title: "Docker Image Optimization: 7 Essential Techniques"
pubDate: "2025-10-10"
description: "Master the 7 essential techniques to shrink your Docker images by 80% or more. Includes practical examples, best practices, and common mistakes to avoid."
tags: ["docker", "optimization", "devops", "containers", "best-practices"]
image: "/images/docker-images-are-too-big.png"
readTime: "8 min read"
---

# Docker Image Optimization: 7 Essential Techniques

Building on our [previous post about Docker image problems and real examples](/blog/docker-optimization-problem-example), let's dive into the 7 essential techniques that will dramatically reduce your Docker image sizes.

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

**Python + Alpine Warning:**
While Alpine images are smaller, they use musl libc instead of glibc, which can cause compatibility issues with Python packages containing C extensions. Many popular packages (numpy, pandas, scipy, etc.) may fail to install or run properly.

### 2. Multi-Stage Builds

Why it matters: Multi-stage builds let you separate build-time dependencies (compilers, dev tools) from runtime dependencies, drastically reducing image size and attack surface. I can also use distroless while using multi-stage builds.

Note: pip install --no-cache-dir or --only-binary is designed to slim Python packages

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

## Best Practices Checklist

- [ ] Use the right image for the job
- [ ] Combine RUN commands to reduce layers
- [ ] Use .dockerignore to exclude unnecessary files
- [ ] Copy only what you need
- [ ] Remove package managers from final image
- [ ] Use multi-stage builds for complex applications
- [ ] Consider distroless images for production
- [ ] Test your optimizations with real applications
- [ ] Monitor image sizes in your CI/CD pipeline
- [ ] Document your optimization decisions

## Common Mistakes to Avoid

1. Installing unnecessary packages
2. Not cleaning up after package installation
3. Copying entire project directories instead of specific files
4. Using large base images when smaller alternatives exist
5. Not using .dockerignore files
6. Leaving build tools in production images
7. Not testing optimizations with real applications

---

## Next Steps

Now that you've mastered the 7 essential techniques, you're ready to learn advanced optimization strategies and powerful analysis tools.

**Continue reading:** [Docker Image Optimization: Advanced Techniques & Tools](/blog/docker-optimization-advanced)

Or go back to the beginning: [Docker Image Optimization: The Problem & Real Example](/blog/docker-optimization-problem-example)
