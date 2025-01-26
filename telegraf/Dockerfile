FROM telegraf:1.19.2

ARG DOCKERIZE_VERSION=v0.6.1
ARG DOCKERIZE_ARCH=amd64

RUN apt update && apt install -y curl sudo
RUN curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
RUN apt install -y speedtest

RUN apt install -y openssl wget 
RUN wget https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-${DOCKERIZE_ARCH}-${DOCKERIZE_VERSION}.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-${DOCKERIZE_ARCH}-${DOCKERIZE_VERSION}.tar.gz \
    && rm dockerize-linux-${DOCKERIZE_ARCH}-${DOCKERIZE_VERSION}.tar.gz

CMD dockerize -wait http://influxdb:8086/ping -timeout 30s telegraf