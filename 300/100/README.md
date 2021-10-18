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
/containers/app/docker-compose.yml
/containers/app/.env
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
sample.env

## 300 - Generate a new app

```
$ npm init react-app sample --use-npm
$ cd sample
```
