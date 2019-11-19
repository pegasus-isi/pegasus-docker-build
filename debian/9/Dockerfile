FROM debian:stretch

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar default-jdk make libmysql-java openmpi-bin libopenmpi-dev bc python-setuptools python-dev python-yaml libssl-dev libpq-dev libmariadb-dev libffi-dev

# Deb package build requirements
RUN apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base default-libmysqlclient-dev libssl1.0-dev python-openssl

# Python requirements
RUN apt-get -y install libsqlite3-dev

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH

WORKDIR /home/bamboo/pegasus-source
