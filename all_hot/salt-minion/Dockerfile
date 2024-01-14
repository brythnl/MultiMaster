FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y salt-minion vim netcat

COPY minion /etc/salt/minion

