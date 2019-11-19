FROM ubuntu:bionic

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN apt-get update

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN apt-get -y install git ant ant-optional gcc g++ tar default-jdk make libmysql-java mpich bc python3-setuptools python3-dev libssl-dev libpq-dev libmysqlclient-dev libffi-dev

# Deb package build requirements
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential debhelper lintian r-base texlive-latex-base texlive-fonts-recommended libssl-dev python3-openssl

# Python requirements
RUN apt-get -y install libsqlite3-dev tox python3-yaml python3-pytest python3-pip

# Documentation
RUN pip3 install sphinx recommonmark sphinx_rtd_theme sphinxcontrib-openapi javasphinx

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH

#RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash && \
#    echo 'export PATH=~/.pyenv/bin:$PATH\neval "$(pyenv init -)"\neval "$(pyenv virtualenv-init -)"' > ~/.bash_profile
#
#RUN pyenv install 2.7.14 && \
#    pyenv install 3.5.5 && \
#    pyenv install 3.6.6 && \
#    pyenv install 3.7.0 && \
#    pyenv global 2.7.14 3.5.5 3.6.6 3.7.0

WORKDIR /home/bamboo/pegasus-source
