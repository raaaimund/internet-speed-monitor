FROM alpine
RUN wget -O - https://bintray.com/ookla/download/download_file?file_path=ookla-speedtest-1.0.0-x86_64-linux.tgz | tar x -f - -z -C /usr/local/bin/ && \
    # change server for speed test by altering value of argument "-s"
    # 3199 - NEXT LAYER GmbH, Vienna, Austria
    echo "*/1 * * * * /usr/local/bin/speedtest --accept-license --accept-gdpr -s 3199 -f json > \$(mktemp -u -p /var/log/speedtest XXXXXX).json" > /etc/crontabs/root
CMD ["crond", "-f", "-d", "8"]
