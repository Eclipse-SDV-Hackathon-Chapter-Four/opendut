FROM ubuntu:22.04

ARG OPENDUT_CARL=https://nc.opendut.net
ARG cannelloni_version=1.1.0
ENV TARGET_TRIPLE=x86_64-unknown-linux-gnu

# Install OS package dependencies. We need:
#   - `can-utils` for `cangw` command used by EDGAR Service
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    tzdata ca-certificates \
    iproute2 bind9-dnsutils iputils-ping fping iptables wireguard-tools tcpdump netcat-traditional \
    curl jq uuid-runtime less vim \
    bridge-utils python3 python3-can can-utils libsctp1 && \
    rm -rf /var/lib/apt/lists/*


# Install cannelloni
RUN mkdir /tmp/cannelloni
WORKDIR /tmp/cannelloni
ADD --checksum=sha256:f98e4cad3a6d1df55423413ea52c676d2eb2ab3d783f25f720654f5797c83c44 \
    https://github.com/eclipse-opendut/cannelloni-build/releases/download/v${cannelloni_version}/cannelloni_manylinux_2_28-x64_${cannelloni_version}.tar.gz \
    /tmp/cannelloni/cannelloni.tar.gz
RUN tar --strip-components=1 -xvf cannelloni.tar.gz

RUN cp libcannelloni-common.so.0 /lib/
RUN cp libsctp.so* /lib/
RUN cp cannelloni /usr/local/bin/


# Bundle EDGAR
WORKDIR /opt/
ADD $OPENDUT_CARL/api/edgar/${TARGET_TRIPLE}/download /opt/opendut-edgar.tar.gz

RUN ls -la /opt
RUN tar xf /opt/opendut-edgar.tar.gz

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

#ENTRYPOINT ["/entrypoint.sh"]

ENTRYPOINT ["sleep", "infinity"]
