FROM debian:buster-slim
# https://crontab.guru/#*/1_*_*_*_*
ARG SPEEDTEST_CRON_SCHEDULE="*/1 * * * *"
# 3199 - NEXT LAYER GmbH, Vienna, Austria
ARG SPEEDTEST_SERVER=3199

RUN apt update && apt install -y curl sudo cron
# install instruction: https://www.speedtest.net/apps/cli
RUN curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
RUN apt install -y speedtest
RUN mkdir /var/log/speedtest
RUN echo "${SPEEDTEST_CRON_SCHEDULE} root /usr/bin/speedtest --accept-license --accept-gdpr -s ${SPEEDTEST_SERVER} -f json > \$(mktemp -u -p /var/log/speedtest XXXXXX).json" > /etc/cron.d/speedtest

CMD ["cron", "-f"]
