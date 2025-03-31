# Dockerfile Explanation and Improvements

## Dockerfile Content

```dockerfile
FROM node:20

WORKDIR /usr/src/app

COPY package* . 
# here all the files that start with `package` are copied to the image thus creating a single layer to govern the change of `package.json` and `package-lock.json` so that they are not uncached due to the change of any other file

RUN npm install 
# This is uncached only if `package.json` or `package-lock.json` changes but remains cached if any other file changes

COPY . . 
# here all the files that don't start with `package` are copied to the image

# ---------------------------- This Dockerfile contains the above 5 layers ----------------------------
EXPOSE 3000

CMD ["node", "index.js"]

# -------------------- End of Dockerfile-------------------------------------------------
```

## Improvements in This Dockerfile

- This Dockerfile solves the first problem in the previous Dockerfile by uncaching the 3rd and 4th layer (`npm install`) only if `package.json` or `package-lock.json` changes, but remains cached if any other file changes.
- The image is still too large (~1.5 GB).

