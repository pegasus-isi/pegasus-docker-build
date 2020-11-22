FROM pegasus/pegasus:focal

MAINTAINER Rajiv Mayani <mayani@isi.edu>, George Papadimitriou <georgpap@isi.edu>

USER root

# Panorama requirements
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get -y install libcurl4-openssl-dev && \
    rm -rf /var/lib/apt/lists/*

USER bamboo
