# Volumes

## What are Volumes

- Volumes are a way to persist data between container restarts.


## The problem it addresses

```sh
docker run -d -p 27017:27017 mongo
```
- This command starts a MongoDB container and maps port 27017 from the host to port 27017 in the container.
- Lets say we do some work using this container as a database.(Write data, read data, etc.)

```sh
docker stop <container_id>
```

```sh
docker start <container_id>
```

- Now the data is still persisted in the container as the container was not deleted.

### Now

```sh
docker kill <container_id>
```

```sh
docker start <container_id>
```

- The data is still persisted in the container as the container was not deleted.

### Now

```sh
docker kill <container_id>
```

```sh
docker rm <container_id>
```

```sh
docker run -d -p 27017:27017 mongo
```

- The data is lost as the container was deleted and restarted.

## Solution

- Volumes are created to persist data between container restarts.

```sh
docker volume create my-mongo-data
```

```sh
# Run the container with the volume my-mongo-data mounted to /data/db of the container
docker run -d -p 27017:27017 -v my-mongo-data:/data/db mongo
```

- Now the data is persisted in the volume my-mongo-data and not in the container.

```sh
docker stop <container_id>
```

```sh
docker start <container_id>
```

- The data is still persisted in the volume my-mongo-data.

```sh
docker kill <container_id>
```

```sh
docker start <container_id>
```

- The data is still persisted in the volume my-mongo-data.

```sh
docker kill <container_id>
```

```sh
docker rm <container_id>
```

```sh
docker run -d -p 27017:27017 -v my-mongo-data:/data/db mongo
```

- The data is still persisted in the volume my-mongo-data.



