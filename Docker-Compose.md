# Docker Compose 

## The problem it addresses

- Let's say you have a multi-container application with multiple services eg a web server and a database.
- By default, you would have to run each container separately using `docker run`.
- And for this you would have to open multiple terminal windows.
- This can be cumbersome and error-prone.
- A possible fix can be to run the containers in the background/detached mode using the `-d` flag.
- But this still requires you to remember the commands for each container.
- Docker Compose provides a solution to this problem by allowing you to define and run multi-container Docker applications using a single YAML file.

## How to use it

Example of a `docker-compose.yml` file for a multi-container application:

```yaml
services:
    mongodb:
        image: mongo:latest
        ports:
            - "27017:27017"
        volumes:
            - mongodb_data:/data/db
    custom_backend:
        build:./
        ports:
            - "3000:3000"
volumes:
    mongodb_data:
```

- The `services` section defines the containers to be run.
- Each service has a name (eg `mongodb`, `custom_backend`).
- The `image` key specifies the base image to use for the container.
- The `build` key specifies the build context for the container (Dockerfile location).
- The `ports` key maps the container ports to the host machine.
- The `volumes` key mounts a volume to the container.
- A `network` is automatically created for the services to communicate with each other using the service name as the hostname.
- To run the application, use the following command:

```sh
docker-compose up
```

- This command reads the `docker-compose.yaml` file and starts the defined services.

## Road Ahead

- Read more docker composes from Open Source projects.
- Here is a [Open Source project for example](https://github.com/processing/p5.js-web-editor)
- Try to understand the `docker-compose.yaml` file present in the repo and how it is used to run the application.
`