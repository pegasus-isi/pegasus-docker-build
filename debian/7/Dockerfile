#
# Note:
# Not configured to run test-pmc.
#

FROM debian:wheezy

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar openjdk-7-jdk make libmysql-java mpich2 bc python-setuptools python-dev libssl-dev libpq-dev libmysqlclient-dev

# Deb package build requirements
RUN apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base dh-python libssl-dev

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

WORKDIR /home/bamboo/pegasus-source
