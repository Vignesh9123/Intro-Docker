# Dockerfile Explanation and Issues

## Dockerfile Content

```dockerfile
FROM node:20 
# node:20 is the base image for this project

WORKDIR /usr/src/app
# this refers to the working dir in the image/container

COPY . . 
# first dot refers to all files in the local system, and second dot refers to the pwd in image/container

RUN npm install 
# This is run when the image is created

# ------------------- This Dockerfile contains the above 4 layers ---------------------------------
EXPOSE 3000
# expose 3000 port of the container to local machine

CMD ["node", "index.js"]
# this is run when the image is converted to container

# -------------------- End of Dockerfile-------------------------------------------------
```

## Problems with this Dockerfile

- Even if `index.js` changes, it results in uncaching the 3rd layer (`COPY . .`) and thus contributes to an increase in build time. Layer 4 (`RUN npm install`) is expensive and should only run if `package.json` changes, but due to the current setup, any file change invalidates Layer 3 and Layer 4, preventing the reuse of cached content in the next build.
- The image is too large (~1.5 GB).

