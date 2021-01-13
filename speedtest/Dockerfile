FROM alpine
RUN wget -O - https://bintray.com/ookla/download/download_file?file_path=ookla-speedtest-1.0.0-x86_64-linux.tgz | tar x -f - -z -C /usr/local/bin/ && \
    # server 5025 - AT&T (Cicero, IL)
    echo "*/15 * * * * /usr/local/bin/speedtest --accept-license -s 5025 -f json > \$(mktemp -u -p /var/log/speedtest XXXXXX).json" > /etc/crontabs/root
CMD ["crond", "-f", "-d", "8"]
