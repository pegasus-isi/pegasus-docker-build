FROM ubuntu:20.04

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN apt update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

RUN DEBIAN_FRONTEND=noninteractive apt -y install \
      ant \
      ant-optional \
      bc \
      build-essential \
      debhelper \
      default-jdk \
      g++ \
      gcc \
      git \
      libffi-dev \
      libmysqlclient-dev \
      libpq-dev \
      libsqlite3-dev \
      libssl-dev \
      lintian \
      mpich \
      python3-dev \
      python3-openssl \
      python3-pip \
      python3-pytest \
      python3-setuptools \
      python3-yaml \
      r-base \
      tar

# Documentation
RUN pip3 install --upgrade pip setuptools==45.3.0 tox

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH

WORKDIR /home/bamboo/pegasus-source
