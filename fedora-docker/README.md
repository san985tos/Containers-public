# Containers Lab

## Instructions

1. Install vagrant on your machine and a supported virtualization tool
2. Download the vagrant machine in this repo
3. Do the following commands

## Commands:

```
# docker pull redis
# docker images
# docker run redis
# docker ps
# docker run -d redis
# docker stop [ID]
# docker start [ID]
# docker ps -a
# docker pull redis:4.0
# docker run -p6000:6379 -d redis
# docker run -p6001:6379 -d redis:4.0
# docker logs
# docker run -d -p6001:6379 --name redis-older redis:4.0
# docker run -d -p6002:6379 --name redis-latest redis
# docker log redis-older
# docker log redis-latest
# docker exec -it [ID] /bin/bash
# docker exec -it redis-older /bin/bash
# docker run -d -v /tmp:/tmp -p6003:6379 --name redis-latest-with-volume redis
```

## Testing Docker root containers:

```
# docker run -d alpine sleep 1d
# pa aux | grep sleep
```

## Add user and add into docker group

```
# su - user
$ docker run -d alpine sleep id
$ echo $UID
```

### A dockerfile

```
From ubuntu:latest
RUN useradd -r -u 1000 -g appuser appuser
USER appuser
ENTRYPOINT ["sleep","infinity"]
```

### Build the new image

```
# docker build -t test
# docker run -d test
# ps aux | grep sleep
# echo vaquita > /tmp/miclave.txt
# chmod 0600 /tmp/miclave.txt
# su - user; cat miclave.txt
# docker run -v /tmp:/tmp -it alpine sh
```

### Inside the container try:

```
# cat /tmp/miclave.txt
```
