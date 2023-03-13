# Partially copied from https://github.com/monero-project/monero/blob/8c3c7b81097b8e260f050b223e7fa3958c14ae66/Dockerfile

FROM ubuntu:20.04 as builder

RUN set -ex && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get --no-install-recommends --yes install \
    automake \
    autotools-dev \
    bsdmainutils \
    build-essential \
    ca-certificates \
    ccache \
    cmake \
    curl \
    git \
    libtool \
    pkg-config \
    gperf

WORKDIR /src

ARG ref=origin/master

RUN git clone --recursive https://github.com/monero-project/monero /src && \
    git reset --hard ${ref} && \
    git submodule sync && git submodule update --init --force --recursive

ARG NPROC
RUN set -ex && \
    git submodule init && git submodule update && \
    rm -rf build && \
    if [ -z "$NPROC" ] ; \
    then make -j$(nproc) depends target=x86_64-linux-gnu ; \
    else make -j$NPROC depends target=x86_64-linux-gnu ; \
    fi


FROM alpine:3.16

RUN apk add --no-cache curl ca-certificates bash

COPY --from=builder /src/build/x86_64-linux-gnu/release/bin /usr/local/bin/


# Create monero user
# RUN adduser --system --group --disabled-password monero && \
#     mkdir -p /wallet /home/monero/.bitmonero && \
#     chown -R monero:monero /home/monero/.bitmonero && \
#     chown -R monero:monero /wallet


# Contains the blockchain
# VOLUME /home/monero/.bitmonero

# Generate your wallet via accessing the container and run:
# cd /wallet
# monero-wallet-cli
# VOLUME /wallet
WORKDIR /var/monero
VOLUME /var/monero

EXPOSE 18080 18081

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]