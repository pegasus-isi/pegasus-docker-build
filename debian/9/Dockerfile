FROM pegasus/pegasus:stretch

MAINTAINER Rajiv Mayani <mayani@isi.edu>, George Papadimitriou <georgpap@isi.edu>

USER root

RUN apt-get update && apt-get upgrade -y

# Panorama requirements
RUN apt-get -y install libcurl4-openssl-dev

USER bamboo
