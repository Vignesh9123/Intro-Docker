# Dockerfile Explanation and Issues

## Dockerfile Content

```dockerfile
FROM mhart/alpine-node # This is the alpine image with node installed in it and is the base image; also, the size of the image is small compared to the node image in the previous Dockerfile

WORKDIR /usr/src/app

COPY package* .

RUN npm install 

COPY . .

# ---------------------------- This Dockerfile contains the above 5 layers ----------------------------
EXPOSE 3000

CMD ["node", "index.js"]

# -------------------- End of Dockerfile-------------------------------------------------
```

## Improvements in This Dockerfile

- The size of the image is smaller (~150 MB).
- This Dockerfile solves both the problems listed in Dockerfile1 by optimizing caching and reducing image size.

