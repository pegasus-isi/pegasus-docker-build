#
# Note:
# Not configured to run dist-doc, test-*.
#

FROM centos:centos5

MAINTAINER Rajiv Mayani <mayani@isi.edu>

RUN yum -y update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install ant ant-nodeps ant-junit gcc gcc-c++ make tar which mpich-devel bc python-setuptools postgresql-devel mysql-devel curl sqlite-devel
RUN yum -y --enablerepo=centosplus install openssl-devel

RUN curl --location --output rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm ; rpm -ivh rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm ; rm --force rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm
RUN yum -y install git jakarta-commons-httpclient jakarta-commons-logging avalon-framework xalan-j2
RUN curl --location --output fop-0.95-1.el5.noarch.rpm http://rpmbin.nogin.org/random_RPMs/RHEL-5/fop-0.95-1.el5.noarch.rpm ; rpm -ivh fop-0.95-1.el5.noarch.rpm ; rm --force fop-0.95-1.el5.noarch.rpm

# RPM Build requirements
# we need both python and python26 to support new and old Pegasus builds
RUN yum -y install rpm-build ant-apache-regexp java7-devel python26 python26-devel python python-devel asciidoc libxslt groff

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo

ENV PATH $PATH:/usr/lib64/mpich/bin

WORKDIR /home/bamboo/pegasus-source
