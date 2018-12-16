## parent image
# open suse
FROM opensuse:latest

## information
# preparation
  # x86_64 processor based hardware
  # required: at least 8GB RAM and about 8GB swap space
  # recommended: at least 16 GB RAM and about 8GB swap space
  # about 100GB free disk space for server installation
  # the SAP AS requires english as the operating system language (LANG=en_US.UTF-8)

## label
LABEL docker.sap.netweaver.dockerfile.description="Docker for SAP NetWeaver AS ABAP 7.52 SP01 Developer Edition - Manual Installation" \
      docker.sap.netweaver.dockerfile.maintainer="mnemotron" \
      docker.sap.netweaver.dockerfile.version="1.0.0" \
      docker.sap.netweaver.dockerfile.date="08.10.2018" \
      docker.sap.netweaver.description="SAP NetWeaver AS ABAP 7.52 SP01 Developer Edition" \
      docker.sap.netweaver.version="7.52 SP01"

## environment
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

## install tools/dependencies
# tcsh         (c shell)
# iputils      (ping for host check)
# net-tools    (contains ifconfig for host check)
RUN zypper --non-interactive install --replacefiles \
      hostname \
      iputils \
      iproute2 \
      nano \
      net-tools \
      systemd \
      tar \
      tcsh \
      unrar \
      wget \
      which

# install and run uuidd daemon
# (universal unique identifiers (UUID) generation daemon, essential for creating database keys, see SAP Note 1310037)
RUN mkdir /run/uuidd && \
    zypper --non-interactive install --replacefiles uuidd && \
    chown uuidd /var/run/uuidd && /usr/sbin/uuidd

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

## prepare installation
# copy uncompressed sap netweaver files into the container
COPY source /tmp/sapnw

# installation script must be executable
RUN chmod +rxw /tmp/sapnw/install.sh

## clean
RUN zypper clean
