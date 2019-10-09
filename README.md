# Docker environment for web push demo

Docker settings for [web-push-demo](https://github.com/tommyheavenly7/web-push-demo), in case if anyone who wants to use node and nginx with SSL for learning push notifications.

## Quick Start Guide

Edit your hosts so that you can use the following as domain names.

```text
0.0.0.0	frontend.local backend.local
```

Next, build and run containers.

```shell script
$ source docker/.bashrc
$ docker-compose build --force-rm --pull --parallel
$ docker-compose up -detach
```

Finally, you can see the demo site.

```text
https://frontend.local/
```

## How to setup the environment

### Edit Your `hosts`

Before you go, edit your hosts so that you can use the following as domain names.
IP address might be different from you case. 
[docker inspect](https://docs.docker.com/engine/reference/commandline/inspect/) might help you in case if the setting doesn't work well.

```text
0.0.0.0	frontend.local backend.local
```

### Configure SSL

You might want to use [mkcert](https://github.com/FiloSottile/mkcert) so that
you can effortlessly setup SSL.

#### 1. Install `mkcert`, if needed

```shell script
$ brew install mkcert
$ brew install nss   # if you use firefox
```

#### 2. Create a new local CA

```shell script
mkcert -install
```

### 3. Created a new certificate

You might want to create two different certificates for both frontend and backend.

```shell script
$ cd ./docker/nginx/ssl
$ mkcert frontend.local "*.frontend.local" frontend nginx localhost 127.0.0.1 0.0.0.0 ::1
$ mkcert backend.local "*.backend.local" backend nginx localhost 127.0.0.1 0.0.0.0 ::1
```

### Prepare for using containers

```shell script
$ source docker/.bashrc
$ docker-compose build --force-rm --pull --parallel
$ docker-compose up --no-start
```

### Install Node dependencies

Before executing the following script, please confirm your `$PATH` contains the path to `./docker/bin`.

```shell script
_run frontend npm install
_run backend npm install
```
Or, you also can directly run the script instead.

```shell script
./docker/bin/_run frontend npm install
./docker/bin/_run backend npm install
```

### Build distribution scripts for frontend

You might be able to find newly created JS files in `./project/frontend/web/dist/*`.

```shell script
_run frontend npm run build
```

## Basic container manipulation

### Run containers

You may see the containers are running.

```shell script
$ docker-compose up --detach
```

### Restart containers

```shell script
docker-compose up -d --force-recreate
```

### Stop containers

```shell script
$ docker-compose stop
```
