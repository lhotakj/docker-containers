FROM phusion/baseimage:jammy-1.0.0

LABEL maintainer="gfjardim <gfjardim@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive
ENV HOME=/root

ARG HAMACHI_VERSION=2.1.0.203
ARG HAMACHI_DL_URL=https://vpn.net/linux/hamachi-${HAMACHI_VERSION}-x64.tgz

ADD sources.list /etc/apt/sources.list

CMD ["/sbin/my_init"]

RUN usermod -u 99 nobody && \
    usermod -g 100 nobody

RUN apt-get update -q

# Install latest Hamachi CLI
ADD ${HAMACHI_DL_URL} /tmp/hamachi.tgz
RUN mkdir -p /opt/logmein-hamachi && \
    tar -zxf /tmp/hamachi.tgz --strip-components 1 -C /opt/logmein-hamachi && \
    ln -sf /opt/logmein-hamachi/hamachid /usr/bin/hamachi && \
    rm /tmp/hamachi.tgz

VOLUME /config

RUN mkdir -p /etc/my_init.d
ADD install.sh /etc/my_init.d/install.sh
RUN chmod +x /etc/my_init.d/install.sh

RUN mkdir -p /etc/service/hamachi
ADD hamachi.sh /etc/service/hamachi/run
RUN chmod +x /etc/service/hamachi/run
