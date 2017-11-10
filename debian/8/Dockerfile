FROM debian:jessie

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar make libmysql-java mpich2 bc python-setuptools python-dev libssl-dev libpq-dev libmysqlclient-dev libffi-dev

# Deb package build requirements
RUN apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base dh-python libssl-dev python-openssl

# Java 8
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && apt-get update && apt-get -y -t jessie-backports install openjdk-8-jdk

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

WORKDIR /home/bamboo/pegasus-source
