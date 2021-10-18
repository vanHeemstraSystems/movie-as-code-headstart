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

Add the following content to the newly created .gitginore file:

```
node_modules
/containers/app/docker-compose.yml
/containers/app/.env
```
.gitignore

## 300 - Generate a new app

```
$ npm init react-app sample --use-npm
$ cd sample
```
