# 400 - React Router and Nginx

If you’re using [React Router](https://reacttraining.com/react-router/), then you’ll need to change the default Nginx config at build time:

Add the following line 
```
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf
```
to containers/app/webui/Dockerfile.prod as follows:

```
ARG IMAGE_REPOSITORY
# development environment: pull official base image for node development
FROM ${IMAGE_REPOSITORY}/node:13.12.0-alpine as build

# See https://stackoverflow.com/questions/29261811/use-docker-compose-env-variable-in-dockerbuild-file
# ARG PROXY_USER
# ARG PROXY_PASSWORD
# ARG PROXY_FQDN
# ARG PROXY_PORT

# ENV HTTP_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"
# ENV HTTPS_PROXY="http://${PROXY_USER}:${PROXY_PASSWORD}@${PROXY_FQDN}:${PROXY_PORT}"

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install app dependencies
COPY package.json ./
COPY package-lock.json ./
RUN npm ci --silent
RUN npm install react-scripts@3.4.1 -g --silent

# add app
COPY . ./

# build app
RUN npm run build

# production environment
FROM ${IMAGE_REPOSITORY}/nginx:stable-alpine

# install build
COPY --from=build /app/build /usr/share/nginx/html

# if using React Router
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

# expose port
EXPOSE 80

# start app
CMD ["nginx", "-g", "daemon off;"]
```
containers/app/webui/Dockerfile.prod

In addition, create the following subdirectory ***nginx*** for nginx configuration:

```
$ cd containers/app/webui
$ mkdir nginx
```

Inside the newly created subdirectory for nginx configuration, create a file called ***sample.nginx.conf***:

```
$ cd containers/app/webui/nginx
$ touch sample.nginx.conf
```

Add the following content to ***sample.nginx.conf***:

```
server {

  listen 80;

  location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
    try_files $uri $uri/ /index.html;
  }

  error_page   500 502 503 504  /50x.html;

  location = /50x.html {
    root   /usr/share/nginx/html;
  }

}
```
containers/app/webui/nginx/sample.nginx.conf

Copy ***sample.nginx.conf***:

```
$ cd containers/app/webui/nginx
$ cp sample.nginx.conf nginx.conf
```
