FROM debian:jessie

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y -t jessie-backports install openjdk-8-jdk libssl-dev
RUN apt-get -y install git ant ant-optional gcc g++ tar make libmysql-java mpich2 bc python-setuptools python-dev libpq-dev libmysqlclient-dev libffi-dev

# Deb package build requirements
RUN apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base dh-python python-openssl

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

WORKDIR /home/bamboo/pegasus-source
