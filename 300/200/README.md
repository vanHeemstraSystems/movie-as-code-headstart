# 200 - Docker for Development Environment

Add a ***Dockerfile*** to the containers/app/webui subdirectory:

```
$ cd containers/app/webui
$ touch Dockerfile
```

Add the following content to the Dockerfile:

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
containers/app/webui/Dockerfile


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
Dockerfile
Dockerfile.prod
```
containers/app/webui/.dockerignore

NOTE: This will speed up the Docker build process as our local dependencies inside the “node_modules” directory will not be sent to the Docker daemon.

== WE ARE HERE ==
