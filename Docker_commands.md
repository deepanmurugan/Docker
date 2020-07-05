### Check docker version
```
docker --version
```

### Docker list images
```
docker images

root@ip-172-31-27-150:/home/ubuntu# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
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

### Information about docker
```
Client:
 Debug Mode: false
Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 19.03.12
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.3.0-1023-aws
 Operating System: Ubuntu 18.04.4 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 1
 Total Memory: 978.8MiB
 Name: ip-172-31-22-94
 ID: ICUT:IFZA:KN7B:G3GS:XA2Q:AURQ:VZUT:QYY7:LVLO:Z5EQ:3MWZ:M2ZQ
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
WARNING: No swap limit support
```

### When you try to pull the same image again
```
root@ip-172-31-22-94:/var/lib/docker# docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
Digest: sha256:35c4a2c15539c6c1e4e5fa4e554dac323ad0107d8eb5c582d6ff386b383b7dce
Status: Image is up to date for ubuntu:latest
docker.io/library/ubuntu:latest
```
```
NOTE: Docker will store the sha256sum of the images in the /var/lib/docker/overlay2 directory and compare if there is any change, once there is a change then only the new docker image is pulled.

Contents in the overlay2 directory after the docker image is pulled.
root@ip-172-31-22-94:/var/lib/docker/overlay2# ls -ltr
total 20
drwx------ 3 root root 4096 Jul  5 05:31 4a7a72c918afdd57689a8d1aa9006e6792cf8f150efbb96fad188cdd7b2cfebd
drwx------ 4 root root 4096 Jul  5 05:31 0c107785142fd98ea6b7efa445aa5f6a054d638d124e853de76bef64d4343376
drwx------ 2 root root 4096 Jul  5 05:31 l
drwx------ 4 root root 4096 Jul  5 05:31 ffc8fdd66a9111faa0fed9824ca5eff88e2553dc852c4ca6157743949efc1970
drwx------ 4 root root 4096 Jul  5 05:31 aab67b11eb2f029483cfe061da2102566c6c0a97e052ade124b1907853145db8
```

### Run a docker image
```
root@ip-172-31-22-94:/var/lib/docker/overlay2# docker run -itd ubuntu
ed73188099fa7e8d5208bb47cb07e0c3af1c541f6d5652c8d1b56d0adf431b50

-i interactive mode
-t putty terminal
-d run as a daemon

root@ip-172-31-22-94:/var/lib/docker/overlay2# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ed73188099fa        ubuntu              "/bin/bash"         8 seconds ago       Up 7 seconds                            laughing_moser

NOTE: NAMES is randomly picked by docker itself. When you don't provide any names docker will pickup random ones.
```

### To Go inside a container
```
root@ip-172-31-22-94:/home/ubuntu# docker exec -it ed73188099fa /bin/bash
root@ed73188099fa:/# 
```















