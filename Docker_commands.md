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
root@ip-172-31-22-94:/home/ubuntu# docker run --name dockerubuntu -itd ubuntu /bin/bash
daa184117390fc0de5e5a1f1402e9103f1a6f8f85324f0ef38a1f544a8137f41
 
root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
daa184117390        ubuntu              "/bin/bash"         4 seconds ago       Up 3 seconds                                  dockerubuntu
195cbc1e045e        tomcat              "catalina.sh run"   6 minutes ago       Up 6 minutes        0.0.0.0:32771->8080/tcp   tomcat-docker
d2e1216a180a        tomcat              "catalina.sh run"   9 minutes ago       Up 9 minutes        0.0.0.0:8080->8080/tcp    upbeat_tereshkova
ed73188099fa        ubuntu              "/bin/bash"         3 hours ago         Up About an hour                              laughing_moser
```

### Delete image when container is up
```
root@ip-172-31-22-94:/home/ubuntu# docker rmi 2e
Error response from daemon: conflict: unable to delete 2eb5a120304e (cannot be forced) - image is being used by running container 195cbc1e045e

Trying to forcefully remove the images

root@ip-172-31-22-94:/home/ubuntu# docker rmi -f 2e
Error response from daemon: conflict: unable to delete 2eb5a120304e (cannot be forced) - image is being used by running container d2e1216a180a

root@ip-172-31-22-94:/home/ubuntu# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
tomcat              latest              2eb5a120304e        3 weeks ago         647MB

Stopping the container and removing the image

root@ip-172-31-22-94:/home/ubuntu# docker container stop d2e1216a180a
d2e1216a180a

root@ip-172-31-22-94:/home/ubuntu# docker rmi -f 2e
Error response from daemon: conflict: unable to delete 2eb5a120304e (cannot be forced) - image is being used by running container 195cbc1e045e
 
root@ip-172-31-22-94:/home/ubuntu# docker stop 195cbc1e045e
195cbc1e045e
 
root@ip-172-31-22-94:/home/ubuntu# docker rmi -f 2e
Untagged: tomcat:latest
Untagged: tomcat@sha256:81c2a95e5b1b5867229d75255abe54928d505deb81c8ff8949b61fde1a5d30a1
Deleted: sha256:2eb5a120304e4e7ab6c901e2ca3ed7ea50e57cd4756818f847b1eaa4d34c3881

root@ip-172-31-22-94:/home/ubuntu# docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
```

### Stop all docker containers/images
```
root@ip-172-31-22-94:/home/ubuntu# docker ps -a -q
daa184117390
d2e1216a180a
ed73188099fa

root@ip-172-31-22-94:/home/ubuntu# docker stop $(docker ps -a -q)
daa184117390
d2e1216a180a
ed73188099fa

root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS               NAMES
daa184117390        ubuntu              "/bin/bash"         5 hours ago         Exited (0) 5 seconds ago                         dockerubuntu
d2e1216a180a        2eb5a120304e        "catalina.sh run"   5 hours ago         Exited (143) 5 seconds ago                       tomcat
ed73188099fa        ubuntu              "/bin/bash"         8 hours ago         Exited (0) 5 seconds ago                         laughing_moser

root@ip-172-31-22-94:/home/ubuntu# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
redis               latest              235592615444        3 weeks ago         104MB

root@ip-172-31-22-94:/home/ubuntu# docker rmi $(docker images -a -q)
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:35c4a2c15539c6c1e4e5fa4e554dac323ad0107d8eb5c582d6ff386b383b7dce
Deleted: sha256:74435f89ab7825e19cf8c92c7b5c5ebd73ae2d0a2be16f49b3fb81c9062ab303
Deleted: sha256:8a8d1f0b34041a66f09e49bdc03e75c2190f606b0db7e08b75eb6747f7b49e11
Deleted: sha256:f1b8f74eff975ae600be0345aaac8f0a3d16680c2531ffc72f77c5e17cbfeeee
Deleted: sha256:27d46ebb54384edbc8c807984f9eb065321912422b0e6c49d6a9cd8c8b7d8ffc
Deleted: sha256:e1c75a5e0bfa094c407e411eb6cc8a159ee8b060cbd0398f1693978b4af9af10
Untagged: redis:latest
Untagged: redis@sha256:800f2587bf3376cb01e6307afe599ddce9439deafbd4fb8562829da96085c9c5
Deleted: sha256:2355926154447ec75b25666ff5df14d1ab54f8bb4abf731be2fcb818c7a7f145
Deleted: sha256:852691351e76013456bccc5ca476ea5998cd4ef829ff88f36aa6152d26752a9f
Deleted: sha256:5638adc92bc136b5d1fa65b5eb75163949c27f9fc372c575ad840b07a19889af
Deleted: sha256:8e68e4829a31a04ca33cdab1c52f2e1dc34ff1eae8f858f87bdb97577e206230
Deleted: sha256:68d6751877f41a67f7fde5abb4c89d3b695df08603299fbf3585d6d1ff09a0e4
Deleted: sha256:7c2052306f31e2f3ba13c29dfff01ca66009d7d44917689662c6bc5ae1725e80
Deleted: sha256:13cb14c2acd34e45446a50af25cb05095a17624678dbafbcc9e26086547c1d74

root@ip-172-31-22-94:/home/ubuntu# docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

### Copy files from host-os to container
```
root@ip-172-31-22-94:/home/ubuntu# cat myfile.txt 
sample file

root@ip-172-31-22-94:/tmp# docker exec 693e088601b4 "cd /tmp && ls -ltr"^C

root@ip-172-31-22-94:/tmp# docker exec -it 693e088601b4 /bin/bash
root@693e088601b4:/# ls -ltr /tmp/
total 4
-rw-r--r-- 1 root root 12 Jul  5 14:18 myfile.txt
```

### Automatically remove docker container when it's stopped
```
root@ip-172-31-22-94:/home/ubuntu# docker run --rm -itd ubuntu
35ec94a38b1398c59eda24edcecc7a93560007122f02d1ee9141c8c2620515fb
 
root@ip-172-31-22-94:/home/ubuntu# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
35ec94a38b13        ubuntu              "/bin/bash"              6 seconds ago       Up 4 seconds                             quizzical_liskov
9d767d45f2d3        customnginx         "/bin/sh -c '/usr/sb…"   6 minutes ago       Up 6 minutes        0.0.0.0:80->80/tcp   eager_bose
6722b5f1ff6f        ubuntu              "/bin/bash"              4 hours ago         Up 4 hours                               gallant_murdock

root@ip-172-31-22-94:/home/ubuntu# docker stop 35ec94a38b13
35ec94a38b13

root@ip-172-31-22-94:/home/ubuntu# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
9d767d45f2d3        customnginx         "/bin/sh -c '/usr/sb…"   6 minutes ago       Up 6 minutes        0.0.0.0:80->80/tcp   eager_bose
6722b5f1ff6f        ubuntu              "/bin/bash"              4 hours ago         Up 4 hours                               gallant_murdock
```

### copy from container to host-os
```
root@ip-172-31-22-94:/tmp# docker cp 693e088601b4:/tmp/myfile.txt .

root@ip-172-31-22-94:/tmp# ls -ltr
total 16
drwx------ 3 root root 4096 Jul  5 05:12 systemd-private-f7c37cd241794c36aa9dcc6e54a97fb7-systemd-timesyncd.service-KKUrt0
drwx------ 3 root root 4096 Jul  5 05:12 systemd-private-f7c37cd241794c36aa9dcc6e54a97fb7-systemd-resolved.service-VZmvbs
drwx------ 2 root root 4096 Jul  5 05:17 tmpdiq0swnv
-rw-r--r-- 1 root root   12 Jul  5 14:18 myfile.txt
```

### Docker container restart based on a condition
```
root@ip-172-31-22-94:/tmp# docker run --restart=always -it ubuntu

root@ip-172-31-22-94:/tmp# docker run --restart=always -it ubuntu

root@33dd1f81d631:/# exit
exit

root@ip-172-31-22-94:/tmp# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
33dd1f81d631        ubuntu              "/bin/bash"         12 seconds ago      Up 1 second                             pedantic_taussig
693e088601b4        ubuntu              "/bin/bash"         11 minutes ago      Up 11 minutes                           ubuntu1804

NOTE: The docker container 33dd1f81d631 exited when using exit command and restarted again as we mentioned restart=always parameter.

Restart allowed values:
--restart=no         | Default value, don't restart the container after it's stopped
--restart=always     | Always restart the container and don't care about the exit code
--restart=on-failure | Restart the container if it fails with non-zero exit code
```

### Remove all stopped docker container
```
root@ip-172-31-22-94:/tmp# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                     PORTS               NAMES
33dd1f81d631        ubuntu              "/bin/bash"         About a minute ago   Exited (0) 5 seconds ago                       pedantic_taussig
693e088601b4        ubuntu              "/bin/bash"         13 minutes ago       Exited (0) 5 seconds ago                       ubuntu1804

root@ip-172-31-22-94:/tmp# docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
33dd1f81d6314577bb04e7e6f7d125a5c6b5e772f43663c972c10094e6327fc5
693e088601b4ee7d2dd22ffb61cdd533a60661dbf54d28f9326d07704780359b
Total reclaimed space: 41B

root@ip-172-31-22-94:/tmp# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

### Get docker container logs
```
root@ip-172-31-22-94:/tmp# docker logs 7742db81f1b0
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /usr/local/openjdk-11
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
NOTE: Picked up JDK_JAVA_OPTIONS:  --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED
....
....

root@ip-172-31-22-94:/tmp# docker logs --tail=2 7742db81f1b0
05-Jul-2020 14:39:17.562 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["http-nio-8080"]
05-Jul-2020 14:39:17.600 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in [201] milliseconds

root@ip-172-31-22-94:/tmp# docker logs --follow 7742db81f1b0

--follow to follow the logs
```

### Search a docker image
```
root@ip-172-31-22-94:/tmp# docker search tomcat
NAME                          DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
tomcat                        Apache Tomcat is an open source implementati…   2770                [OK]                
tomee                         Apache TomEE is an all-Apache Java EE certif…   79                  [OK]                
dordoka/tomcat                Ubuntu 14.04, Oracle JDK 8 and Tomcat 8 base…   54                                      [OK]
bitnami/tomcat                Bitnami Tomcat Docker Image                     35                                      [OK]
kubeguide/tomcat-app          Tomcat image for Chapter 1                      28                                      
```

### Commit custom image after changes
```
root@ip-172-31-22-94:/home/ubuntu# docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB

root@ip-172-31-22-94:/home/ubuntu# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
6722b5f1ff6f        ubuntu              "/bin/bash"              4 hours ago         Up 4 hours                               gallant_murdock

root@ip-172-31-22-94:/home/ubuntu# docker exec -it 67 bash

root@6722b5f1ff6f:/# apt-get update -y

root@6722b5f1ff6f:/# apt-get install nginx -y

root@ip-172-31-22-94:/home/ubuntu# docker commit -m "custom nginx" -c 'CMD /usr/sbin/nginx -g "daemon off;" ' -c 'EXPOSE 80' 6722b5f1ff6f customnginx

root@ip-172-31-22-94:/home/ubuntu# docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
customnginx         latest              dc52ed60c93d        3 seconds ago       218MB
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB

root@ip-172-31-22-94:/home/ubuntu# docker run -itd -p 80:80 customnginx
9d767d45f2d348717ecd6c300bd52d1ce846ea83c00582ea0e7b480c8623745a

root@ip-172-31-22-94:/home/ubuntu# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
9d767d45f2d3        customnginx         "/bin/sh -c '/usr/sb…"   4 seconds ago       Up 3 seconds        0.0.0.0:80->80/tcp   eager_bose
6722b5f1ff6f        ubuntu              "/bin/bash"              4 hours ago         Up 4 hours                               gallant_murdock
```

### Build image from docker file
```
root@ip-172-31-22-94:/home/ubuntu/dockerfiles# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB

root@ip-172-31-22-94:/home/ubuntu/dockerfiles# cat dockerfile 
FROM ubuntu:18.04

RUN apt-get update -y
RUN apt-get install nginx -y
RUN rm /var/www/html/index*
COPY index.html /var/www/html

EXPOSE 80
CMD /usr/sbin/nginx -g "daemon off;"

root@ip-172-31-22-94:/home/ubuntu/dockerfiles# docker build -t ubuntu-nginx .

root@ip-172-31-22-94:/home/ubuntu/dockerfiles# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu-nginx        latest              97cdbc524379        15 seconds ago      153MB
ubuntu              latest              74435f89ab78        2 weeks ago         73.9MB
ubuntu              18.04               8e4ce0a6ce69        2 weeks ago         64.2MB
```

### Check image history
```
root@ip-172-31-22-94:/home/ubuntu/dockerfiles# docker history ubuntu-nginx
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
97cdbc524379        8 minutes ago       /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "/usr…   0B                  
edf535435fce        8 minutes ago       /bin/sh -c #(nop)  EXPOSE 80                    0B                  
aff321c5566c        8 minutes ago       /bin/sh -c #(nop) COPY file:372a886dc338c388…   620B                
e3dfa4883093        8 minutes ago       /bin/sh -c rm /var/www/html/index*              0B                  
c32b10781415        8 minutes ago       /bin/sh -c apt-get install nginx -y             60.3MB              
a2a07c86637d        8 minutes ago       /bin/sh -c apt-get update -y                    28.9MB              
8e4ce0a6ce69        2 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           2 weeks ago         /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           2 weeks ago         /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B                
<missing>           2 weeks ago         /bin/sh -c [ -z "$(apt-get indextargets)" ]     987kB               
<missing>           2 weeks ago         /bin/sh -c #(nop) ADD file:1e8d02626176dc814…   63.2MB       
```

### Login to docker hub
```
docker login
```

### Push docker images to docker hub
```
root@ip-172-31-22-94:/home/ubuntu# docker tag ubuntu-nginx:latest deepanmurugan/cloudrepo:nginx-v1.0.0

root@ip-172-31-22-94:/home/ubuntu# docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
deepanmurugan/cloudrepo   nginx-v1.0.0        97cdbc524379        53 minutes ago      153MB
ubuntu-nginx              latest              97cdbc524379        53 minutes ago      153MB
ubuntu                    latest              74435f89ab78        2 weeks ago         73.9MB
ubuntu                    18.04               8e4ce0a6ce69        2 weeks ago         64.2MB

root@ip-172-31-22-94:/home/ubuntu# docker push deepanmurugan/cloudrepo:nginx-v1.0.0
The push refers to repository [docker.io/deepanmurugan/cloudrepo]
bad0de65784d: Pushed 
19adfc54695f: Pushed 
a2786e07fe53: Pushed 
abd92d1b5326: Pushed 
ddc500d84994: Mounted from library/ubuntu 
c64c52ea2c16: Mounted from library/ubuntu 
5930c9e5703f: Mounted from library/ubuntu 
b187ff70b2e4: Mounted from library/ubuntu 
nginx-v1.0.0: digest: sha256:30d20db8432c119f809999a51a12fed6a942b1187b39a5009d66defe1f56bd57 size: 1990
```

### Pull image from docker hub
```
root@ip-172-31-22-94:/home/ubuntu# docker pull deepanmurugan/cloudrepo:nginx-v1.0.0
```

### Save docker image as a file
```
root@ip-172-31-22-94:/home/ubuntu# docker save -o nginx.tgz deepanmurugan/cloudrepo:nginx-v1.0.0

root@ip-172-31-22-94:/home/ubuntu# ls -ltr
total 152884
drwxr-xr-x 2 root root      4096 Jul  6 09:55 dockerfiles
-rw------- 1 root root 156544000 Jul  6 10:57 nginx.tgz
```

### Launch docker image from a file
```
root@ip-172-31-22-94:/home/ubuntu# docker load < nginx.tgz
Loaded image: deepanmurugan/cloudrepo:nginx-v1.0.0

root@ip-172-31-22-94:/home/ubuntu# docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
deepanmurugan/cloudrepo   nginx-v1.0.0        97cdbc524379        59 minutes ago      153MB
ubuntu-nginx              latest              97cdbc524379        59 minutes ago      153MB
ubuntu                    latest              74435f89ab78        2 weeks ago         73.9MB
ubuntu                    18.04               8e4ce0a6ce69        2 weeks ago         64.2MB
```
