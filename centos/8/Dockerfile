FROM pegasus/pegasus:centos8

MAINTAINER Rajiv Mayani <mayani@isi.edu>, George Papadimitriou <georgpap@isi.edu>

USER root

# Panorama requirements
RUN yum -y update && \
    yum -y install curl-devel && \
    yum clean all && \
    rm -rf /var/cache/yum

USER bamboo
