# 100 - Project Setup

## 100 - Install Create React App globally

```
$ npm install -g create-react-app@3.4.1
```

## 200 - Setup the directory structure

For flexibility and maintenance of configuration let us first set up the directory structure.

Make a .gitignore file in the root of the project: 

```
$ touch .gitignore
```

Add the following content to the newly created .gitignore file:

```
node_modules
/containers/app/docker-compose.dev.yml
/containers/app/docker-compose.prod.yml
/containers/app/.env
/containers/app/webui/nginx/nginx.conf
```
.gitignore

Add a ***containers*** directory from the root of the project.

```
$ mkdir containers
```

Add an ***app*** directory from within the containers directory.

```
$ cd containers
$ mkdir app
```

Inside the app directory create a ***sample environment*** file.

```
$ cd app
$ touch sample.env
```

With the sample.env file created, add the following content to it:

```
IMAGE_REPOSITORY=docker.io
PROXY_USER=my-proxy-user
PROXY_PASSWORD=my-proxy-password
PROXY_FQDN=my-proxy.my-company.com
PROXY_PORT=8080
```
containers/app/sample.env

Inside the app directory create a ***sample.docker-compose.dev.yml*** file.

```
$ cd app
$ touch sample.docker-compose.dev.yml
```

With the sample.docker-compose.dev.yml file created, add the following content to it:

```
version: "3.7"

# See https://stackoverflow.com/questions/29261811/use-docker-compose-env-variable-in-dockerbuild-file
services:

  webui:
    build:
      context: ./webui
      dockerfile: Dockerfile.dev
      args: # from env_file
        IMAGE_REPOSITORY: ${IMAGE_REPOSITORY}
        PROXY_USER: ${PROXY_USER}
        PROXY_PASSWORD: ${PROXY_PASSWORD}
        PROXY_FQDN: ${PROXY_FQDN}
        PROXY_PORT: ${PROXY_PORT}
    env_file:
      - .env
    container-name: webui-dev  
    ports:
      - "8080:3000"
    volumes:
      - ./webui:/app
      - /app/node_modules
    environment:
      - CHOKIDAR_USEPULLING=true
```
containers/app/sample.docker-compose.dev.yml

## 300 - Generate a new app

Inside the subdirectory /containers/app/ created a new app called '***webui***':

```
$ cd containers/app
$ npm init react-app webui --use-npm
$ cd webui
```

You will be prompted as follows:

```
found 27 vulnerabilities (8 moderate, 18 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details

Success! Created webui at /Users/willemvanheemstra/git/movie-as-code-headstart/containers/app/webui
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd webui
  npm start

Happy hacking!
```

Take care of the reported vulnerabilities by running the following command from within the webui directory.

```
$ cd webui
$ npm audit fix
```
