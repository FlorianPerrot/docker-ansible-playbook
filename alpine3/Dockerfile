FROM alpine:3.15.4

MAINTAINER Florian Perrot <me@florian-perrot.fr>

# From https://github.com/William-Yeh/docker-ansible by William Yeh <william.pjyeh@gmail.com> 
RUN echo "===> Installing sudo to emulate normal OS behavior..."  && \
    apk --update add sudo                                         && \
    \
    \
    echo "===> Adding Python runtime..."  && \
    apk --update add python py-pip openssl ca-certificates    && \
    apk --update add --virtual build-dependencies \
                python-dev libffi-dev openssl-dev build-base  && \
    pip install --upgrade pip cffi                            && \
    \
    \
    echo "===> Installing Ansible..."  && \
    pip install ansible                && \
    \
    \
    echo "===> Installing handy tools (not absolutely required)..."  && \
    pip install --upgrade pycrypto pywinrm         && \
    apk --update add sshpass openssh-client rsync  && \
    \
    \
    echo "===> Removing package list..."  && \
    apk del build-dependencies            && \
    rm -rf /var/cache/apk/*               && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    echo 'localhost' > /etc/ansible/hosts

RUN apk --update add git && \
    rm -rf /var/cache/apk/* 

# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]
