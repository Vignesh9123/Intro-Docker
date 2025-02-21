# Multi Stage Builds

## The problem it addresses

- There can be instances where you need to run a different set of commands when you are working in development vs. when you are deploying to production.
- For example, you might need to run nodemon in development but not in production.
- You can use multi-stage builds to create a smaller image for production and smaller image for development both when required use a base image and then build on top of it.

## How to use it

Example of a multi-stage build for a Node.js app:

```Dockerfile
FROM node:20 AS base
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install

FROM base AS development
COPY . .
CMD ["npm", "run", "dev"]

FROM base AS production
COPY . .
CMD ["npm","run","start"]
```

- The first `FROM` instruction creates a base image with the Node.js image.
- The second `FROM` instruction creates a development image on top of the base image that copies the source code and runs `npm run dev`.
- The third `FROM` instruction creates a production image on top of the base image that copies the source code and runs `npm run start`.

To build the development image:

```sh
docker build -t my-node-app:dev --target development .
```

To build the production image:

```sh
docker build -t my-node-app:prod --target production .
```
- The run command after this is the same as usual.

## Another problem regarding nodemon here

- Running the above image using `docker run <options> my-node-app:dev` will not work as expected (i.e nodemon will not restart the server when changes are made locally).
- This is because changes made to the source code on the host machine are not reflected in the container.
- To solve this, you can use a bind mount to mount the source code from the host machine to the container.

```sh
docker run -v .:/usr/src/app -p 4000:4000 my-node-app:dev
```

- This command mounts the current directory to `/usr/src/app` in the container and runs the development image.
- Now, changes made to the source code on the host machine will be reflected in the container and nodemon will restart the server when changes are made.
- Note that now the changes made in the *container* will also be reflected in the *host* machine.

