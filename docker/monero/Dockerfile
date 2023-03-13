FROM alpine:3.16

RUN apk add --no-cache curl ca-certificates bash

WORKDIR /var/monero

RUN cd /
RUN curl 'https://downloads.getmonero.org/cli/monero-linux-x64-v0.18.2.0.tar.bz2' -O
RUN ls -la

COPY --from=builder /src/build/bin/monerod /monerod

VOLUME /var/monero

EXPOSE 18080 18081 18083

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
