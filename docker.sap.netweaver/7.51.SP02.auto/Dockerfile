## parent image
# ubuntu
FROM ubuntu:18.04

## information
# preparation
  # x86_64 processor based hardware
  # required: at least 8GB RAM and about 8GB swap space
  # recommended: at least 16 GB RAM and about 8GB swap space
  # about 100GB free disk space for server installation
  # the SAP AS requires english as the operating system language (LANG=en_US.UTF-8)

## label
LABEL docker.sap.netweaver.dockerfile.description="Docker for SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition - Automatic Installation" \
      docker.sap.netweaver.dockerfile.maintainer="mnemotron" \
      docker.sap.netweaver.dockerfile.version="1.0.0" \
      docker.sap.netweaver.dockerfile.date="08.10.2018" \
      docker.sap.netweaver.description="SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition" \
      docker.sap.netweaver.version="7.51 SP02"

## install tools/dependencies
# csh          (c shell)
# expect       (to automatically run through the SAP installation script)
# iputils-ping (ping for host check)
# libaio1      (linux kernel AIO access library, SAP Sybase ASE requires the library to start the installation)
# locales...   (language settings)
# net-tools    (contains ifconfig for host check)
RUN apt-get update && \
    apt-get install -y \
      csh \
      expect \
      iputils-ping \
      libaio1 \
      locales locales-all \
      net-tools

# install and run uuidd daemon
# (universal unique identifiers (UUID) generation daemon, essential for creating database keys, see SAP Note 1310037)
RUN mkdir /run/uuidd && \
    apt-get install -y uuid-runtime && \
    chown uuidd /var/run/uuidd && /usr/sbin/uuidd

## environment
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

## ports
# 8000/TCP  (HTTP)
# 44300/TCP (HTTPS)
# 8443/TCP  (SAP cloud connector)
# 3200/TCP  (SAP GUI)
# 3300/TCP  (RFC)
EXPOSE 8000/tcp \
       44300/tcp \
       8443/tcp \
       3200/tcp \
       3300/tcp

# copy uncompressed sap netweaver files into the container
COPY source /tmp/sapnw

## workdir
WORKDIR /tmp/sapnw

## prepare installation
# installation script must be executable
RUN chmod +rwx install.sh && \
    sed -i 's/| more//g' ./install.sh

# build enhanced installation script (based on expect)
# password: pSAPNW
RUN echo '#!/usr/bin/expect -f\n \
    spawn ./install.sh -s -k\n \
      set PASSWORD "pSAPNW"\n \
      set timeout -1\n \
    expect "Hit enter to continue!"\n \
      send "\\r" \
    expect "Do you agree to the above license terms? yes/no:"\n \
      send "yes\\r"\n \
    expect "Please enter a password:"\n \
      send "$PASSWORD\\r"\n \
    expect "Please re-enter password for verification:"\n \
      send  "$PASSWORD\\r"\n \
    expect eof' >> ./einstall.sh; chmod +x ./einstall.sh

## run enhanced installation script
RUN ./einstall.expp

## clean
RUN apt-get purge expect && \
    apt-get -y clean && \
    apt-get -y autoremove && \
    apt-get -y autoclean && \
    rm -rf /tmp/sapnw && \
    rm -rf /var/lib/apt/lists/*
