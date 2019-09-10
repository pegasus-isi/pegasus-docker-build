FROM centos:centos7

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN yum -y update | /bin/true

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install ant | /bin/true
RUN yum -y install git ant-junit gcc gcc-c++ tar make bc mpich-devel python-setuptools openssl-devel postgresql-devel mysql-devel libxml2 epel-release libffi-devel yum-plugin-priorities libuuid-devel libseccomp-devel squashfs-tools cryptsetup wget golang

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java-1.7.0-openjdk-devel java-1.8.0-openjdk-devel python-devel pyOpenSSL which R-devel groff asciidoc libxslt fop

# Python requirements
RUN yum -y install gcc patch readline-devel zlib-devel bzip2-devel sqlite-devel python-pip PyYAML pytest && \
    pip install --upgrade pip setuptools && \
    pip install tox

# Container requirements (Singularity installation)
RUN export VERSION=1.11 OS=linux ARCH=amd64 && \
    wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
    tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
    rm go$VERSION.$OS-$ARCH.tar.gz 

ENV GOPATH /home/bamboo/go
ENV PATH /usr/local/go/bin:$PATH:$GOPATH/bin

RUN go get -u github.com/golang/dep/cmd/dep

RUN yum -y install vim 

RUN export VERSION=3.2.0 && \
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

#RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash && \
#    echo -e 'export PATH=~/.pyenv/bin:$PATH\neval "$(pyenv init -)"\neval "$(pyenv virtualenv-init -)"' > ~/.bash_profile
#
#RUN pyenv install 2.6.9 && \
#    pyenv install 2.7.14 && \
#    pyenv install 3.3.7 && \
#    pyenv install 3.4.8 && \
#    pyenv install 3.5.5 && \
#    pyenv install 3.6.6 && \
#    pyenv install 3.7.0 && \
#    pyenv global 2.6.9 2.7.14 3.3.7 3.4.8 3.5.5 3.6.6 3.7.0

WORKDIR /home/bamboo/pegasus-source
