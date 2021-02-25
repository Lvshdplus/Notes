# Docker with SSH

## 1. Manually Configure

1. **System Requirement**: ubuntu (differs from centos)

2. **prerequisite** 

   ```shell
   apt-get install -y vim openssh-server
   ```

3. **Set Login password**

   ```shell
   # 1
   passwd root
   
   # 2
   echo "user:password" | chpassed
   ```

4. **Modify Config file**

   ```shell
   # change PermitRootLogin prohibit-password to PermitRootLogin yes
   vim /etc/ssh/sshd_config
   ```

5. **Restart SSH**

   ```shell
   /etc/init.d/ssh restart
   ```

6. **Map Docker Port**

   ```shell
   # ssh default port is 22
   docker run -d --name containerName -p hostPort:dockerPort(22) imageID
   ```

7. **Login Remotely**

   ```shell
   ssh ip -l root -p portNumber
   ```

   

## 2. Write into Dockerfile

1. **Dockerfile**

```dockerfile
FROM ubuntu:20.04
MAINTAINER Shidong<shidonglyu@gmail.com>

# worke space
ENV MYPATH /home/
WORKDIR $MYPATH

# install tools
RUN apt-get update
#RUN apt-get install -y git build-essential make gcc vim net-tools iputils-ping openssh-server manpages-dev
RUN apt-get install -y openssh-server
RUN apt-get install -y vim
# set password
RUN echo "root:12345" | chpasswd

# repalce "PermitRootLogin prohibit-password" with "PermitRootLogin yes" in file: /etc/ssh/sshd_config
#RUN sed -i 's/prohibit-password/yes/' /etc/ssh/sshd_config
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config


EXPOSE 8080 9090

# start ssh service
RUN mkdir /var/run/sshd
#ENTRYPOINT ["/usr/sbin/sshd","-D"]

CMD ["/usr/sbin/sshd", "-D"]

```

2. **Build Image**

```shell
docker build -t imageName[:TAG] .
```

3. **Run Image** 

```shell
# run docker in detached mode
# map default ssh port 22 to hostPort(you can choose)
docker run -d --name lsd -p 8080:22 test
```



## 3. Q&A

1. when docker changes, fingerprint may also change, delete original fingerpint from knownHost
2. when installing 