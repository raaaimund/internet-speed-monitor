FROM debian:buster-slim
RUN apt update && apt install -y curl sudo cron
# install instruction: https://www.speedtest.net/apps/cli
RUN curl -s https://install.speedtest.net/app/cli/install.deb.sh | sudo bash
RUN apt install speedtest
RUN mkdir /var/log/speedtest
# change server for speed test by altering value of argument "-s"
# 3199 - NEXT LAYER GmbH, Vienna, Austria
# https://crontab.guru/#*/1_*_*_*_*
RUN echo "*/1 * * * * root /usr/bin/speedtest --accept-license --accept-gdpr -s 3199 -f json > \$(mktemp -u -p /var/log/speedtest XXXXXX).json" > /etc/cron.d/speedtest
CMD ["cron", "-f"]
