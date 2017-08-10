FROM centos:centos7

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN yum -y update | /bin/true

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install ant | /bin/true
RUN yum -y install git ant-junit gcc gcc-c++ tar make bc mpich-devel python-setuptools openssl-devel postgresql-devel mysql-devel libxml2 epel-release

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java-1.8.0-openjdk-devel python-devel pyOpenSSL which R-devel groff asciidoc libxslt fop

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

ENV PATH $PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
