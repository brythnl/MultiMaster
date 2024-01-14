FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y salt-master vim

COPY master /etc/salt/master

EXPOSE 4505 4506

