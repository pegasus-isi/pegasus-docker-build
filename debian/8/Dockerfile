FROM debian:jessie

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar make libmysql-java mpich2 bc python-setuptools python-dev libssl-dev libpq-dev libmysqlclient-dev libffi-dev

# Deb package build requirements
RUN apt-get -y install build-essential debhelper asciidoc fop xsltproc lintian r-base dh-python libssl-dev python-openssl

# Java 8
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && apt-get update && apt-get -y -t jessie-backports install openjdk-8-jdk
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Python requirements
RUN apt-get -y install libsqlite3-dev python-tox

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH $HOME/.pyenv/bin:$PATH

RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash && \
    echo 'export PATH=~/.pyenv/bin:$PATH\neval "$(pyenv init -)"\neval "$(pyenv virtualenv-init -)"' > ~/.bash_profile

RUN pyenv install 2.6.9 && \
    pyenv install 2.7.14 && \
    pyenv install 3.3.7 && \
    pyenv install 3.4.8 && \
    pyenv install 3.5.5 && \
    pyenv install 3.6.6 && \
    pyenv global 2.6.9 2.7.14 3.3.7 3.4.8 3.5.5 3.6.6

WORKDIR /home/bamboo/pegasus-source
