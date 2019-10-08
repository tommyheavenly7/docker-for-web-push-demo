# Docker environment for web push demo

## Configure SSL

You might want to use [mkcert](https://github.com/FiloSottile/mkcert) so that
you can effortlessly setup SSL.

### Install `mkcert`, if needed

```shell script
$ brew install mkcert
$ brew install nss   # if you use firefox
```

### Create a new local CA

```shell script
mkcert -install
```

### Created a new certificate

You might want to create two different certificates for both frontend and backend.

```shell script
$ cd ./docker/nginx/ssl
$ mkcert frontend.local "*.frontend.local" frontend nginx localhost 127.0.0.1 0.0.0.0 ::1
$ mkcert backend.local "*.backend.local" backend nginx localhost 127.0.0.1 0.0.0.0 ::1
```

## Container manipulation

### Prepare for using containers

```shell script
$ source docker/.bashrc
$ docker-compose build --force-rm --pull
$ docker-compose up --no-start
```

### Run containers

You may see the nginx container is running.

```shell script
$ docker-compose up --detach
```
