# Yandex.Tank 1.7.32
#
# Documentation link is https://github.com/yandex/yandex-tank/blob/v1.7.32/docs/

FROM ubuntu:xenial
MAINTAINER Anton Shapin <shapin.anton@gmail.com>

LABEL Description="Yandex.Tank version is 1.7.32 from github tag v1.7.32 with phantom and Jmeter" Vendor="Yandex" Version="0.0.1"

#Install Java 8
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java8-installer && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/oracle-jdk8-installer

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

#Install ssh server
RUN apt-get update -y && \
    apt-get install  -y apt-utils && \
    apt-get install ssh -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Install phantom
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y sudo && \
    apt-get install -y wget && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:yandex-load/main -y && \
    apt-get update && apt-get install -y python-pip phantom phantom-ssl

#Install yandex-tank version 1.7.32
RUN BUILD_DEPS="python-dev build-essential gfortran libssl-dev libffi-dev" && \
    apt-get install -y ${BUILD_DEPS} && \
    pip install --upgrade pip && \
    pip install  --upgrade setuptools && \
    pip install https://github.com/yandex/yandex-tank/archive/v1.7.32.zip && \
    apt-get autoremove -y ${BUILD_DEPS} && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Install module ReportOnline(https://github.com/yandex-load/yatank-online)
RUN pip install yatank-online && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Install Jmeter
RUN apt-get update && \
    apt-get install -y jmeter && \
    apt-get clean

VOLUME ["/var/loadtest"]
WORKDIR /var/loadtest
ENTRYPOINT ["/usr/local/bin/yandex-tank"]
