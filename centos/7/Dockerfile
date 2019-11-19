FROM centos:centos7

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN yum -y update | /bin/true

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install ant | /bin/true
RUN yum -y install git ant-junit gcc gcc-c++ tar make bc mpich-devel python-setuptools openssl-devel postgresql-devel mysql-devel libxml2 epel-release libffi-devel yum-plugin-priorities libuuid-devel libseccomp-devel squashfs-tools cryptsetup wget golang

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java-1.8.0-openjdk-devel python-devel pyOpenSSL which R-devel groff asciidoc libxslt fop

# Python requirements
RUN yum -y install gcc patch readline-devel zlib-devel bzip2-devel sqlite-devel python-pip PyYAML && \
    pip install --upgrade pip setuptools && \

# Container requirements (Singularity installation)
RUN export VERSION=1.11 OS=linux ARCH=amd64 && \
    wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
    tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
    rm go$VERSION.$OS-$ARCH.tar.gz

ENV GOPATH /home/bamboo/go
ENV PATH /usr/local/go/bin:$PATH:$GOPATH/bin

RUN go get -u github.com/golang/dep/cmd/dep

RUN export VERSION=3.0.1 && \
    mkdir -p $GOPATH/src/github.com/sylabs && \
    cd $GOPATH/src/github.com/sylabs && \
    wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
    tar -xzf singularity-${VERSION}.tar.gz && \
    rm singularity-${VERSION}.tar.gz && \
    cd ./singularity && \
    ./mconfig && \
    make -C ./builddir && \
    make -C ./builddir install

# Set templates in magic file so that Singularity files can be identified using the 'file' command
RUN echo $'# using env \n\
0	string/t	#!/usr/bin/env		a \n\
>15	string/t	>\\0			%s script text executable \n\
!:strength / 10 \n\
\n\
0	string/b	#!/usr/bin/env		a \n\
>15	string/b	>\\0			%s script executable (binary data) \n\
!:strength / 10 \n\
\n\
0	string/t	#!\ /usr/bin/env	a \n\
>16	string/t	>\\0			%s script text executable \n\
!:strength / 10 \n\
\n\
0	string/b	#!\ /usr/bin/env	a \n\
>16	string/b	>\\0			%s script executable (binary data) \n\
!:strength / 10' >> /etc/magic

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
