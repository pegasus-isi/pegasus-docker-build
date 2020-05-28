FROM centos:8

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

# we should't really need this, but for some reason we do to install ant-junit
RUN echo 'module_hotfixes=true' >>/etc/yum.repos.d/CentOS-PowerTools.repo

# clean rpm database
RUN rm -f /var/lib/rpm/Pubkeys && \
    rpm --rebuilddb

RUN dnf -y update && \
    dnf -y install 'dnf-command(config-manager)' && \
    yum -y config-manager --set-enabled PowerTools && \
    dnf -y install epel-release

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

RUN dnf -y install --allowerasing --nobest \
    ant-apache-regexp \
    ant-junit \
    bc \
    bzip2-devel \
    gcc \
    gcc-c++ \
    git \
    java-11-openjdk-devel \
    libffi-devel \
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
    zlib-devel \
    glibc-langpack-en

# Python test requirements - FIXME: not a great idea to use pip3 install in this container
RUN pip3 install tox

# Documentation - FIXME: not a great idea to use pip3 install in this container
RUN pip3 install sphinx recommonmark sphinx_rtd_theme sphinxcontrib-openapi javasphinx

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

ENV LC_ALL="en_US.UTF-8"

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
