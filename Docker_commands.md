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

### Stop/Start Docker container
```
root@ip-172-31-22-94:/home/ubuntu# docker stop ed73188099fa
ed73188099fa

root@ip-172-31-22-94:/home/ubuntu# docker container ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
ed73188099fa        ubuntu              "/bin/bash"         2 hours ago         Exited (0) 3 seconds ago                       laughing_moser

root@ip-172-31-22-94:/home/ubuntu# docker start ed73188099fa
ed73188099fa

root@ip-172-31-22-94:/home/ubuntu# docker container ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ed73188099fa        ubuntu              "/bin/bash"         2 hours ago         Up 3 seconds                            laughing_moser
```

### Check running docker container stats
```
root@ip-172-31-22-94:/home/ubuntu# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
360b7607875e        ubuntu              "/bin/bash"         2 minutes ago       Up 2 minutes                            confident_wu
ccad34d73eb5        ubuntu              "/bin/bash"         2 minutes ago       Up 2 minutes                            unruffled_bardeen
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up 7 minutes                            laughing_moser

root@ip-172-31-22-94:/home/ubuntu# docker stats
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
360b7607875e        confident_wu        0.00%               1.234MiB / 978.8MiB   0.13%               726B / 0B           0B / 0B             1
ccad34d73eb5        unruffled_bardeen   0.00%               1.328MiB / 978.8MiB   0.14%               726B / 0B           233kB / 0B          1
ed73188099fa        laughing_moser      0.00%               1.477MiB / 978.8MiB   0.15%               1.16kB / 0B         2.94MB / 0B         1
```

### See docker config and other details
```
root@ip-172-31-22-94:/home/ubuntu# docker inspect ed73188099fa
```

### Remove docker container forcefully
```
root@ip-172-31-22-94:/home/ubuntu# docker rm 360b7607875e
Error response from daemon: You cannot remove a running container 360b7607875ee197c48ab9e82373014606d4ee062b8224900c0f16c2c4cfae38. Stop the container before attempting removal or force remove

root@ip-172-31-22-94:/home/ubuntu# docker rm -f 360b7607875e
360b7607875e

root@ip-172-31-22-94:/home/ubuntu# docker container ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ccad34d73eb5        ubuntu              "/bin/bash"         12 minutes ago      Up 12 minutes                           unruffled_bardeen
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up 17 minutes                           laughing_moser
```

### Remove docker images
```
root@ip-172-31-22-94:/home/ubuntu# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
tomcat              latest              2eb5a120304e        3 weeks ago         647MB
 
root@ip-172-31-22-94:/home/ubuntu# docker rmi tomcat
Untagged: tomcat:latest
Untagged: tomcat@sha256:81c2a95e5b1b5867229d75255abe54928d505deb81c8ff8949b61fde1a5d30a1
Deleted: sha256:2eb5a120304e4e7ab6c901e2ca3ed7ea50e57cd4756818f847b1eaa4d34c3881
Deleted: sha256:020e9c85f973b9633036443c8608cf7f3172d711173ff7af930673087ea3d887
Deleted: sha256:813a36f23140b157a76870e5b5b91c191a39fd938d8015bade6ca671062b759c
Deleted: sha256:52f06f71d56ef812d695e8069da6b175d3a8095dfc5da3949e0c872411a617e0
Deleted: sha256:c9ef80d5f34210a78113974f64ce32386f5c28a6cf538c398daf76052d2abf99
Deleted: sha256:e313f84ea12ee09cf103147b76bf2fb372d40ccfed273e2389e96a56fb31e11e
Deleted: sha256:15239410c554dafb7f891f0d51def4992ead6d7307b4f224241d1c685b7ce493
Deleted: sha256:f863ffb247f4c239aeccf155b7c0d92e35403aed0c825690f6739a89a5901a7c
Deleted: sha256:d39c04f36d47ec7121d94577c33c2792aa6e5a5a2c1130ea0be67a96d4e42ba5
Deleted: sha256:7ef5d661de63acc27e877ff7098e93fd9d915f9688e8b585af1b3cccafd76243
Deleted: sha256:8803ef42039dcbe936755e9baae4bb7b19cb0fb6a438eb3992950cd0afef8e4f
```

### Map docker container port with Host OS port
```
docker run -itd -p 8080:8080 tomcat

-p maps host-os port with container port
-P randomly maps host-os port with container port

root@ip-172-31-22-94:/home/ubuntu# netstat -nptl
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      733/systemd-resolve 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1048/sshd           
tcp6       0      0 :::8080                 :::*                    LISTEN      13697/docker-proxy  
tcp6       0      0 :::22                   :::*                    LISTEN      1048/sshd           

root@ip-172-31-22-94:/home/ubuntu# docker run -itd -P tomcat
195cbc1e045ea56eeb3a068fa2cce763752e0f82ba1efe9de2dcfcc16483a091

root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS                     NAMES
195cbc1e045e        tomcat              "catalina.sh run"   5 seconds ago       Up 5 seconds                  0.0.0.0:32771->8080/tcp   gracious_hertz
fca67a78ec6a        tomcat              "catalina.sh run"   25 seconds ago      Exited (130) 17 seconds ago                             frosty_maxwell
d2e1216a180a        tomcat              "catalina.sh run"   3 minutes ago       Up 3 minutes                  0.0.0.0:8080->8080/tcp    upbeat_tereshkova
ccad34d73eb5        ubuntu              "/bin/bash"         51 minutes ago      Up 51 minutes                                           unruffled_bardeen
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up 56 minutes                                           laughing_moser

root@ip-172-31-22-94:/home/ubuntu# netstat -nptl
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      733/systemd-resolve 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1048/sshd           
tcp6       0      0 :::8080                 :::*                    LISTEN      13697/docker-proxy  
tcp6       0      0 :::22                   :::*                    LISTEN      1048/sshd           
tcp6       0      0 :::32771                :::*                    LISTEN      14044/docker-proxy  
```

### Change name of any container
```
root@ip-172-31-22-94:/home/ubuntu# docker rename gracious_hertz tomcat-docker

root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
195cbc1e045e        tomcat              "catalina.sh run"   3 minutes ago       Up 3 minutes        0.0.0.0:32771->8080/tcp   tomcat-docker
d2e1216a180a        tomcat              "catalina.sh run"   6 minutes ago       Up 6 minutes        0.0.0.0:8080->8080/tcp    upbeat_tereshkova
ccad34d73eb5        ubuntu              "/bin/bash"         55 minutes ago      Up 55 minutes                                 unruffled_bardeen
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up 59 minutes                                 laughing_moser
```

### Provide custom name while launching a container
```
root@ip-172-31-22-94:/home/ubuntu# docker run -itd --name dockerubuntu ubuntu /bin/bash
daa184117390fc0de5e5a1f1402e9103f1a6f8f85324f0ef38a1f544a8137f41
 
root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
daa184117390        ubuntu              "/bin/bash"         4 seconds ago       Up 3 seconds                                  dockerubuntu
195cbc1e045e        tomcat              "catalina.sh run"   6 minutes ago       Up 6 minutes        0.0.0.0:32771->8080/tcp   tomcat-docker
d2e1216a180a        tomcat              "catalina.sh run"   9 minutes ago       Up 9 minutes        0.0.0.0:8080->8080/tcp    upbeat_tereshkova
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up About an hour                              laughing_moser
```












