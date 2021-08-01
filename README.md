# Monitor your internet speed

with [speedtest.net][1], [Grafana][2], [Telegraf][3], [InfluxDB][4] and [Docker][5].

Original https://github.com/raaaimund/internet-speed-monitor was outdated, and several thing didn´t work anymore.
Fixed them.

Thanks raaaimund for the great setup! Just had to fix some dependencies of yours!


After running 

```
docker-compose up
```

Docker starts the following services

* influxdb
    * store for our speed test results
* speedtester
    * schedules a cron job for running a speed test using the official [speedtest.net cli][6] every five minutes to JSON log files
    * you can change the specified server and interval in the corresponding [Dockerfile][7]
* telegraf
    * reads the JSON logs with the results and sends them to influxdb
* grafana
    * visualises our results on a simple preconfigured dashboard
    * default credentials are admin:admin

## Change speedtest server

Change the value of the ``-s`` argument in the [.env](./speedtest/Dockerfile) file to alter the server on which to perform the speed test. You can list nearby servers with ``speedtest -L``.

[1]: https://www.speedtest.net/
[2]: https://grafana.com/
[3]: https://www.influxdata.com/time-series-platform/telegraf/
[4]: https://www.influxdata.com/
[5]: https://www.docker.com/
[6]: https://www.speedtest.net/apps/cli
[7]: speedtest/Dockerfile
