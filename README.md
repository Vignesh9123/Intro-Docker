# Docker Optimization Examples

This repository demonstrates the progressive optimization of a Dockerfile for a Node.js application through three different implementations. Each version addresses specific issues and shows improvements in build efficiency and image size.

## Repository Structure

- [Dockerfile1.md](./Dockerfile1.md) - Basic implementation with common issues
- [Dockerfile2.md](./Dockerfile2.md) - Improved caching strategy
- [Dockerfile3.md](./Dockerfile3.md) - Optimized implementation with smaller base image

## Evolution of the Dockerfiles

### 1. Basic Implementation (Dockerfile1)
- Uses `node:20` as base image
- Demonstrates common issues in Dockerfile creation
- Problems:
  - Inefficient caching (unnecessary rebuilds)
  - Large image size (~1.5 GB)

### 2. Improved Caching (Dockerfile2)
- Still uses `node:20` as base image
- Implements better layer caching by:
  - Separating package files copying
  - Optimizing the order of operations
- Improvements:
  - Better build performance through efficient caching
  - Still has large image size (~1.5 GB)

### 3. Optimized Implementation (Dockerfile3)
- Uses `mhart/alpine-node` as base image
- Maintains efficient caching strategy
- Improvements:
  - Significantly reduced image size (~150 MB)
  - Optimal caching behavior
  - Production-ready implementation

## Key Learnings
- Proper layer ordering is crucial for build performance
- Base image selection significantly impacts final image size
- Separating dependency installation from application code improves caching
- Alpine-based images provide a good balance of functionality and size

## Usage
Each Dockerfile variant is documented in its respective markdown file, including:
- Complete Dockerfile content
- Detailed explanations of each instruction
- Specific improvements and remaining issues

Review each implementation to understand the progression of optimizations and choose the approach that best suits your needs.

---

## Volumes
- Refer to [Volumes.md](./Volumes.md) for detailed information on volumes in Docker.

## Networks
- Refer to [Networks.md](./Networks.md) for detailed information on networks in Docker.