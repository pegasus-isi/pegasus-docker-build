FROM centos:centos6

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN yum -y update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install java-1.8.0-openjdk git ant ant-nodeps ant-junit gcc gcc-c++ tar which mpich-devel bc python-setuptools postgresql-devel mysql-devel epel-release libffi-devel
RUN yum -y --enablerepo=centosplus install openssl-devel

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java-1.7.0-openjdk-devel java-1.8.0-openjdk-devel python-devel pyOpenSSL asciidoc libxslt fop R

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

ENV PATH $PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
