FROM telegraf:1.19.2
ENV DOCKERIZE_VERSION=v0.6.1
RUN apt-get update && apt-get install -y openssl wget 
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
CMD dockerize -wait http://influxdb:8086/ping -timeout 30s telegraf