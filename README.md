# Monitor your internet speed

with [speedtest.net][1], [Grafana][2], [Telegraf][3], [InfluxDB][4] and [Docker][5].

Original https://github.com/raaaimund/internet-speed-monitor was outdated, and several things didn´t work anymore.
Fixed them. Thanks to @raaaimund for the great setup! Just had to fix some dependencies of yours!

This project is fixed to the ``x86`` architecture.

After running 

```
docker-compose up
```

Docker starts the following services

* influxdb
    * store for the speed test results
* speedtester
    * schedules a cron job for running a speed test using the official [speedtest.net cli][6] every five minutes to JSON log files
    * you can change the specified server and interval in the corresponding [Dockerfile][7]
* telegraf
    * reads the JSON logs with the results and sends them to influxdb
* grafana
    * visualizes the results on a simple pre-configured dashboard
    * default credentials are **admin:admin**

## Change speedtest server and cron schedule

Change the value of the ``SPEEDTEST_SERVER`` and ``SPEEDTEST_CRON_SCHEDULE`` arguments in the [.env](.env) file to alter the server on which to perform the speed test. You can list servers with ``speedtest -L``. The default values are ``SPEEDTEST_SERVER=3199`` and ``SPEEDTEST_CRON_SCHEDULE="*/1 * * * *"``.

Thanks to @timokluser-dev for this PR.

[1]: https://www.speedtest.net/
[2]: https://grafana.com/
[3]: https://www.influxdata.com/time-series-platform/telegraf/
[4]: https://www.influxdata.com/
[5]: https://www.docker.com/
[6]: https://www.speedtest.net/apps/cli
[7]: speedtest/Dockerfile
