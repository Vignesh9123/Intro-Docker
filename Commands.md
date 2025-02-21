# Docker Commands Reference  

## Building Images  

```sh
# Build an image from a Dockerfile (run this in the directory containing the Dockerfile)
docker build -t my-node-app .
```

```sh
# Build with a specific Dockerfile
docker build -t my-node-app -f Dockerfile1 .
docker build -t my-node-app -f Dockerfile2 .
docker build -t my-node-app -f Dockerfile3 .
```

## Running Containers  

```sh
# Run the container (maps port 3000 from host to container (left is host, right is container))
docker run -p 3000:3000 my-node-app
```

```sh
# Run in detached mode (background)
docker run -d -p 3000:3000 my-node-app
```

## Container Management  

```sh
# List running containers
docker ps
```

```sh
# List all containers (including stopped)
docker ps -a
```

```sh
# Stop a running container
docker stop <container_id>
```

```sh
# Remove a container
docker rm <container_id>
```

## Image Management  

```sh
# List all images
docker images
```

```sh
# Remove an image
docker rmi my-node-app
```

```sh
# Remove unused images
docker image prune
```

## Environment Variables  

```sh
# Run container with environment variables
docker run -e PORT=4000 -p 4000:4000 my-node-app
```

```sh
# Run container with environment variables from a file
docker run --env-file .env -p 4000:4000 my-node-app
```

- The `.env` file should contain key-value pairs in the format `KEY=VALUE`.
- There is a better way to manage environment variables using Docker Compose.

## Debugging & Logs  

```sh
# View container logs
docker logs <container_id>
```

## Layer & Cache Management  

```sh
# View build history and layers
docker history my-node-app
```

## Useful Tips  

```sh
# To rebuild without using cache
docker build --no-cache -t my-node-app .
```

```sh
# To see the size of images
docker images my-node-app
```

```sh
# Execute commands in running container
docker exec -it <container_id> /bin/bash
```

```sh
# Copy files between host and container
docker cp <file> <container_id>:/path/to/destination
docker cp <container_id>:/path/to/file ./local-destination
```

## Example Workflow  

```sh
# 1. Build the optimized image (using Dockerfile3)
docker build -t my-node-app -f Dockerfile3 .
```

```sh
# 2. Run the container in detached mode
docker run -d -p 3000:3000 my-node-app
```

```sh
# 3. Check if container is running
docker ps
```

```sh
# 4. View logs
docker logs <container_id>
```

```sh
# 5. Stop container when done
docker stop <container_id>
```

