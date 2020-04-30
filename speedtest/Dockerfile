FROM python:3-alpine
WORKDIR /usr/speedtest
RUN pip install --no-cache-dir speedtest-cli && \
    speedtest-cli --csv-header > speedtest-results.csv && \
    # server 3744 - Nessus GmbH (10G Uplink) (Vienna, Austria)
    echo "*/5 * * * * speedtest-cli --server 3744 --secure --csv >> /usr/speedtest/speedtest-results.csv" > /etc/crontabs/root
CMD ["crond", "-f", "-d", "8"]