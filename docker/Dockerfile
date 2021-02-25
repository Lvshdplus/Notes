FROM ubuntu:20.04
MAINTAINER Shidong<shidonglyu@gmail.com>

# env virables
ENV MYPATH /home/
ENV TZ=Asia/Hong_Kong
# worke space
WORKDIR $MYPATH

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install tools
# RUN apt-get update && apt-get install -y \
#     openssh-server \
#     vim \
#     && rm -rf /var/lib/apt/lists/*

# install tools
RUN apt-get update && apt-get install -y \
  git \
  build-essential \
  make \
  gcc \
  vim \
  net-tools \
  iputils-ping \
  manpages-dev \
  openssh-server \
  vim \
  && rm -rf /var/lib/apt/lists/*

# set password
RUN echo "root:12345" | chpasswd

# repalce "PermitRootLogin prohibit-password" with "PermitRootLogin yes" in file: /etc/ssh/sshd_config
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

RUN apt-get clean && \
    rm -rf /tmp/* /var/tmp/* 
# start ssh service
# RUN service restart ssh
RUN mkdir /var/run/sshd
CMD ["/usr/sbin/sshd", "-D"]

#CMD ["/bin/bash"]