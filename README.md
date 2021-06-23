# TODO
simple todo list manager
- running in Node.js
- packaged with Docker

See the `Dockerfile` in the same folder as the file `package.json` with the following contents:
```docker
FROM node:12-alpine
RUN apk add --no-cache python g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

build the container image using the `docker build` command.
```
docker build -t getting-started .
```

We started from the `node:12-alpine` image. Since we didn't have that on our machine, that image got downloaded.

After the image was downloaded, we copied in our application and used `yarn` to install our application's dependencies. The `CMD` directive specifies the default command to run when starting a container from this image.

Finally, the `-t` flag tags our image. Think of this simply as a human-readable name for the final image. Since we named the image `todo`, we can refer to that image when we run a container.

The `.` at the end of the docker build command tells that Docker should look for the `Dockerfile` in the current directory.

Start your container using the docker run command and specify the name of the image we just created:
```
docker run -dp 5500:3000 todo
```
Remember the `-d` and `-p` flags? We're running the new container in "detached" mode (in the background) and creating a mapping between the host's port `5500` to the container's port `3000`. Without the port mapping, we wouldn't be able to access the application.

After a few seconds, open your web browser to http://localhost:5500. You should see our app!