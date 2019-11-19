FROM ubuntu:bionic

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar default-jdk make libmysql-java mpich bc python-setuptools python-dev libssl-dev libpq-dev libmysqlclient-dev libffi-dev

# Deb package build requirements
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base libssl-dev python-openssl python3-openssl

# Python requirements
RUN apt-get -y install libsqlite3-dev python-yaml

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH

WORKDIR /home/bamboo/pegasus-source
