FROM centos:8

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

# we should't really need this, but for some reason we do to install ant-junit
RUN echo 'module_hotfixes=true' >>/etc/yum.repos.d/CentOS-PowerTools.repo

RUN dnf -y update && \
    dnf -y install 'dnf-command(config-manager)' && \
    yum -y config-manager --set-enabled PowerTools && \
    dnf -y install epel-release

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

RUN dnf -y install --allowerasing --nobest \
     ant \
     ant-apache-regexp \
     ant-junit \
     asciidoc \
     bc \
     bzip2-devel \
     gcc \
     gcc-c++ \
     git \
     groff \
     java-11-openjdk-devel \
     libffi-devel \
     libxml2 \
     libxslt \
     make \
     mpich-devel \
     mysql-devel \
     openssl-devel \
     patch \
     postgresql-devel \
     python3-devel \
     python3-pyOpenSSL \
     python3-pytest \
     python3-pyyaml \
     R-devel \
     readline-devel \
     rpm-build \
     sqlite-devel \
     tar \
     which \
     zlib-devel

# Python requirements
RUN pip3 install --upgrade pip setuptools && \
    pip install tox

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
