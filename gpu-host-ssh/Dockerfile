FROM ubuntu:24.04 AS build_apt
SHELL ["/bin/bash", "-c"]
LABEL maintainer="nxt5656@live.cn"
RUN apt update && apt install -y \
    make \
    git \
    python3 \
    python3-pip \
    wget \
    curl \
    nano \
    vim \
    supervisor \
    easy-rsa \
    openssh-server \
    passwd \
    net-tools

FROM build_apt AS base
LABEL org.opencontainers.image.source=https://github.com/nxt5656/devops-docker-images
LABEL org.opencontainers.image.description="容器基础镜像"
LABEL org.opencontainers.image.licenses=MIT
WORKDIR /workspace
ADD --chmod=600 supervisord.conf /devops/supervisord.conf
RUN mkdir /var/run/sshd
RUN ssh-keygen -A
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
RUN echo "root:UserPas$0w" | chpasswd
ENTRYPOINT ["supervisord","-c","/devops/supervisord.conf"]