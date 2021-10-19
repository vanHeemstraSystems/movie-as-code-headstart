# 400 - React Router and Nginx

If you’re using [React Router](https://reacttraining.com/react-router/), then you’ll need to change the default Nginx config at build time:

Add the following line to containers/app/webui/Dockerfile.prod as follows:

```


```
containers/app/webui/Dockerfile.prod

In addition, create the following subdirectory ***nginx*** for nginx configuration:

```
$ cd containers/app/webui
$ mkdir nginx
```

Inside the newly created subdirectory for nginx configuration, create a file called ***nginx.conf***:

```
$ cd containers/app/webui/nginx
$ touch nginx.conf
```

Add the following content to ***nginx.conf***:

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
containers/app/webui/nginx/nginx.conf
