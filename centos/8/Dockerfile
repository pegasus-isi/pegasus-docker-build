FROM pegasus/pegasus:centos8

MAINTAINER Rajiv Mayani <mayani@isi.edu>, George Papadimitriou <georgpap@isi.edu>

USER root

# Panorama requirements
#RUN dnf -y --allowerasing update && \
RUN dnf -y install curl-devel && \
    dnf clean all && \
    rm -rf /var/cache/yum

USER bamboo
