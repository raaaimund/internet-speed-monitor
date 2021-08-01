FROM alpine
RUN apk update && apk add curl sudo speedtest-cli
#RUN curl -s https://install.speedtest.net/app/cli/install.deb.sh | sudo sh
#RUN sudo apt-get install speedtest && \
    # change server for speed test by altering value of argument "-s"
    # 3199 - NEXT LAYER GmbH, Vienna, Austria
RUN echo "*/1 * * * * /usr/bin/speedtest --json > \$(mktemp -u -p /var/log/speedtest XXXXXX).json" > /etc/crontabs/root
CMD ["crond", "-f", "-d", "8"]
