FROM ubuntu:20.04

RUN cp /etc/apt/sources.list /etc/apt/sources.backup.list

# Please comment this line if you are not using Tencent Cloud network
#COPY sources.list /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y cmake gdb python python3 vim emacs locales
RUN apt-get install -y curl sudo
RUN useradd -m csapp && \
    echo "root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    echo "csapp ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers 
RUN locale-gen en_US.UTF-8

ENV LANG=en_US.utf8 \
    LANGUAGE=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

RUN curl -fOL github.com.cnpmjs.org/cdr/code-server/releases/download/v3.10.2/code-server_3.10.2_amd64.deb && \
    dpkg -i code-server_3.10.2_amd64.deb

RUN apt-get install -y net-tools
RUN usermod -s /bin/bash csapp
RUN chsh -s /bin/bash csapp
ENV SHELL=/bin/bash 

RUN apt-get install -y cgdb git

# DataLab
RUN apt-get install -y g++-multilib

# ArchLab
RUN apt-get install -y flex bison libgetopt-complete-perl

# CacheLab
RUN apt-get install -y valgrind

# Network Packages
RUN apt-get install -y aria2

# PDF Extension: Not working
# ADD tomoki1207.pdf-1.1.0.tar /home/csapp/.local/share/code-server/extensions/
# RUN chown csapp -R /home/csapp/.local/share/

USER csapp

# TODO: C++ Extension

# PDF: Not working as well
# RUN code-server --install-extension tomoki1207.pdf

# Formatter Extension
RUN code-server --install-extension esbenp.prettier-vscode

USER root

RUN chown csapp -R /home/csapp/.local/share/

RUN cp /etc/apt/sources.list /etc/apt/sources-tencent.list
RUN mv /etc/apt/sources.backup.list /etc/apt/sources.list
RUN apt-get update

EXPOSE 7777

ENV PASSWORD=csapp

USER csapp

CMD [ "code-server", "--bind-addr", "0.0.0.0:7777", "--auth", "password" ]
