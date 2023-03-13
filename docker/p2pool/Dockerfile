FROM alpine:latest

RUN apk add --no-cache curl jq bash wget tar

RUN mkdir -p /p2pool
RUN cd p2pool
RUN wget https://github.com/SChernykh/p2pool/releases/download/v3.1/p2pool-v3.1-linux-x64.tar.gz
RUN tar –xvzf p2pool-v3.1-linux-x64.tar.gz
RUN mv p2pool-v3.1-linux-x64/* .

EXPOSE 3333 37889

WORKDIR /p2pool/data

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
