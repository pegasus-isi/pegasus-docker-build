FROM centos:centos6

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN yum -y update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install git ant ant-nodeps ant-junit gcc gcc-c++ tar which mpich-devel bc python-setuptools postgresql-devel mysql-devel
RUN yum -y --enablerepo=centosplus install openssl-devel

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java7-devel python-devel asciidoc libxslt fop

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

ENV PATH $PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
