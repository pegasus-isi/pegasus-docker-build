FROM centos:centos7

LABEL maintainer="Rajiv Mayani <mayani@isi.edu>, Mats Rynge <rynge@isi.edu>"

RUN yum -y update | /bin/true

RUN useradd --gid 100 --uid 550 --create-home --password bamboo123 bamboo

# Test requirements
RUN yum -y install ant | /bin/true
RUN yum -y install git ant-junit gcc gcc-c++ tar make bc mpich-devel python-setuptools openssl-devel postgresql-devel mysql-devel libxml2 epel-release libffi-devel

# RPM Build requirements
RUN yum -y install rpm-build ant-apache-regexp java-1.7.0-openjdk-devel java-1.8.0-openjdk-devel python-devel pyOpenSSL which R-devel groff asciidoc libxslt fop

# Python requirements
RUN yum -y install gcc patch readline-devel zlib-devel bzip2-devel sqlite-devel && \
    easy_install pip PyYAML && \
    pip install --upgrade pip setuptools && \
    pip install tox

# Set Timezone
RUN cp /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

USER bamboo

RUN mkdir /home/bamboo/.pegasus

ENV HOME /home/bamboo
ENV PATH $HOME/.pyenv/bin:$PATH:/usr/lib64/mpich/bin

RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash && \
    echo -e 'export PATH=~/.pyenv/bin:$PATH\neval "$(pyenv init -)"\neval "$(pyenv virtualenv-init -)"' > ~/.bash_profile

RUN pyenv install 2.6.9 && \
    pyenv install 2.7.14 && \
    pyenv install 3.3.7 && \
    pyenv install 3.4.8 && \
    pyenv install 3.5.5 && \
    pyenv install 3.6.6 && \
    pyenv install 3.7.0 && \
    pyenv global 2.6.9 2.7.14 3.3.7 3.4.8 3.5.5 3.6.6 3.7.0

WORKDIR /home/bamboo/pegasus-source
