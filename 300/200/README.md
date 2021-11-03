# 200 - Docker for Development Environment

Add a ***Dockerfile.dev*** to the containers/app/webui subdirectory:

```
$ cd containers/app/webui
$ touch Dockerfile.dev
```

Add the following content to the Dockerfile.dev:

```
ARG IMAGE_REPOSITORY
# pull official base image
FROM ${IMAGE_REPOSITORY}/node:13.12.0-alpine

# See https://stackoverflow.com/questions/29261811/use-docker-compose-env-variable-in-dockerbuild-file
ARG PROXY_USER
ARG PROXY_PASSWORD
ARG PROXY_FQDN
ARG PROXY_PORT

ENV HTTP_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"
ENV HTTPS_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install app dependencies
COPY package.json ./
COPY package-lock.json ./
RUN npm install --silent
RUN npm install react-scripts@3.4.1 -g --silent

# add app
COPY . ./

# start app
CMD ["npm", "start"]
```
containers/app/webui/Dockerfile.dev

If you run into an "ENOENT: no such file or directory, open '/app/package.json". error, you may need to add an additional volume: -v /app/package.json.

NOTE: Silencing the NPM output, via --silent, is a personal choice. It’s often frowned upon, though, since it can swallow errors. Keep this in mind so you don’t waste time debugging.

Add a ***.dockerignore*** file in the same directory.

```
$ cd containers/app/webui
$ touch .dockerignore
```

Add the following content to the .dockerignore file

```
node_modules
build
.dockerignore
Dockerfile.dev
Dockerfile.prod
```
containers/app/webui/.dockerignore

NOTE: This will speed up the Docker build process as our local dependencies inside the “node_modules” directory will not be sent to the Docker daemon.

Copy sample files:

```
$ cd containers/app
$ cp sample.env .env
$ cp sample.docker-compose.dev.yml docker-compose.dev.yml
```

Make sure Docker Engine is installed:

```
$ docker version
```

Make sure docker-compose is installed:

```
$ docker-compose version
```

Make sure Docker daemon is up and running:

```
sudo systemctl start docker
sudo service docker start
```

NOTE: If you are ***not*** behind a proxy, comment out these entries in the Dockerfile.dev:

```
# See https://stackoverflow.com/questions/29261811/use-docker-compose-env-variable-in-dockerbuild-file
# ARG PROXY_USER
# ARG PROXY_PASSWORD
# ARG PROXY_FQDN
# ARG PROXY_PORT

# ENV HTTP_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"
# ENV HTTPS_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"
```

Get a recent version of docker-compose:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Build and tag the Docker image, and run the container specifying its name as "movie-as-code-dev" to distinguish it from possible other stacks that are called "app" (the default name, based on the root directory):

```
$ cd containers/app
$ docker-compose --file docker-compose.dev.yml --project-name movie-as-code-dev up --build -d
```

**Note**:   
```
-p, --project-name NAME     Specify an alternate project name
                              (default: directory name)
```                              

If successful, you can browse to the start page of the new React App, which will look like below:

![Screenshot 2021-10-19 at 13 07 46](https://user-images.githubusercontent.com/1499433/137897955-908a2483-66c2-4ab8-a22a-a8a06ca6b325.png)

http://localhost:8080

What’s happening here?

1. The ***docker-compose*** command creates and runs a new container instance from the image we just created.

2. -v ./webui:/app mounts the code into the container at “/app”.

3. Since we want to use the container version of the “node_modules” folder, we configured another volume: -v /app/node_modules. You should now be able to remove the local “node_modules” flavor.

4. -p 8080:3000 exposes port 3000 to other Docker containers on the same network (for inter-container communication) and port 8080 to the host.

5. Finally, environment: - CHOKIDAR_USEPOLLING=true enables a polling mechanism via chokidar (which wraps fs.watch, fs.watchFile, and fsevents) so that hot-reloading will work.

Take note of the volumes. Without the anonymous volume ('/app/node_modules'), the node_modules directory would be overwritten by the mounting of the host directory at runtime. In other words, this would happen:

- Build - The node_modules directory is created in the image.
- Run - The current directory is mounted into the container, overwriting the node_modules that were installed during the build.

Hot-reloading

Test hot-relaoding by making a change to containers/app/webui/src/App.js and watch how the browser reloads to show the change automatically.

Bring down the container before moving on:

```
$ docker-compose --file docker-compose.dev.yml stop
```
