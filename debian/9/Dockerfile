FROM pegasus/pegasus:4.9-stretch

MAINTAINER Rajiv Mayani <mayani@isi.edu>, George Papadimitriou <georgpap@isi.edu>

USER root

RUN apt-get update && apt-get upgrade -y

# Panorama requirements
RUN apt-get -y install libcurl4-openssl-dev

USER bamboo
