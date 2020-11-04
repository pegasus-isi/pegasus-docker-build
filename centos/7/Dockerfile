FROM centos:centos7

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN yum -y update | /bin/true

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install epel-release
RUN yum -y install ant | /bin/true
RUN yum -y install \
     ant-apache-regexp \
     ant-junit \
     bc \
     bzip2-devel \
     cryptsetup \
     epel-release \
     gcc \
     gcc-c++ \
     git \
     golang \
     java-1.8.0-openjdk-devel \
     libffi-devel \
     libseccomp-devel \
     libuuid-devel \
     make \
     mpich-devel \
     mysql-devel \
     openssl-devel \
     patch \
     postgresql-devel \
     python36-attr \
     python36-devel \
     python36-GitPython \
     python36-pip \
     python36-pyOpenSSL \
     python36-pytest \
     python36-PyYAML \
     python36-setuptools \
     R-devel \
     readline-devel \
     rpm-build \
     singularity \
     sqlite-devel \
     squashfs-tools \
     tar \
     wget \
     which \
     yum-plugin-priorities \
     zlib-devel 

# Python test requirements - FIXME: not a great idea to use pip3 install in this container
RUN pip3 install tox

# Documentation - FIXME: not a great idea to use pip3 install in this container
RUN pip3 install sphinx recommonmark sphinx_rtd_theme sphinxcontrib-openapi javasphinx

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
