FROM alpine:3.16

RUN apk add --no-cache curl ca-certificates bash

WORKDIR /var/monero

RUN cd /
RUN curl 'https://downloads.getmonero.org/cli/monero-linux-x64-v0.18.2.0.tar.bz2' -O
RUN tar -xvf monero-linux-x64-v0.18.2.0.tar.bz2
RUN mv -v monero-x86_64-linux-gnu-v0.18.2.0/* .

VOLUME /var/monero

EXPOSE 18080 18081 18083

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
