### Check docker version
```
docker --version
```

### Docker list images
```
docker images

root@ip-172-31-27-150:/home/ubuntu# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        5 days ago          73.9MB
```

### Pull docker image from docker repository
```
docker pull ubuntu

Using default tag: latest
latest: Pulling from library/ubuntu
a4a2a29f9ba4: Pull complete 
127c9761dcba: Pull complete 
d13bf203e905: Pull complete 
4039240d2e0b: Pull complete 
Digest: sha256:35c4a2c15539c6c1e4e5fa4e554dac323ad0107d8eb5c582d6ff386b383b7dce
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

### List all running docker containers
```
docker container ps
(or)
docker ps
```

### List all docker containers
```
docker container ps -a
(or)
docker ps -a
```

### Docker default path
```
root@ip-172-31-22-94:/home/ubuntu# cd /var/lib/docker/
root@ip-172-31-22-94:/var/lib/docker# ls -ltr
total 48
drwx------ 2 root root 4096 Jul  5 05:18 runtimes
drwx------ 2 root root 4096 Jul  5 05:18 containers
drwx------ 4 root root 4096 Jul  5 05:18 plugins
drwx------ 2 root root 4096 Jul  5 05:18 volumes
drwx------ 3 root root 4096 Jul  5 05:18 image
drwx------ 2 root root 4096 Jul  5 05:18 trust
drwxr-x--- 3 root root 4096 Jul  5 05:18 network
drwx------ 2 root root 4096 Jul  5 05:18 swarm
drwx------ 3 root root 4096 Jul  5 05:18 overlay2
drwx------ 2 root root 4096 Jul  5 05:18 builder
drwx--x--x 4 root root 4096 Jul  5 05:18 buildkit
drwx------ 2 root root 4096 Jul  5 05:18 tmp
```







