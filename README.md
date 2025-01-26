# Monitor your internet speed

with [speedtest.net][1], [Grafana][2], [Telegraf][3], [InfluxDB][4] and [Docker][5].

After running

```bash
docker-compose up
```

Docker starts the following services

* ``influxdb``
  * store for the speed test results
* ``telegraf``
  * runs speed tests using the official [speedtest.net cli][6] every five minutes using the [exec input plugin][9]
  * sends the result to influxdb using the [influxdb output plugin][12]
* ``grafana``
  * visualizes the results on a simple pre-configured dashboard
  * default credentials are **admin:admin**
  * dashboad is available on <http://localhost:3000/d/speedtest/speedtest>

## Adapt speedtest configuration

The docker container ``telegraf`` uses the [exec input plugin][9] to execute the speedtest. Change the [telegraf.conf][10] file to adapt the speedtest config. Also check the [.env][11] file for setting the interval and used server for the speedtest. You can list servers with ``speedtest -L``.

Thanks to [@timokluser-dev][13] for [PR #7][15] and [@Bedasek][14] for [Issue #9][16].

## ARM

I used a Raspberry Pi 3B+ with [Hypriot][8] for running the internet speed monitor.
To run this on a device with an ARM architecture (e.g. Raspberry Pi) run the following command

```bash
docker-compose -f docker-compose.yaml -f docker-compose.arm.yaml up
```

[1]: https://www.speedtest.net/
[2]: https://grafana.com/
[3]: https://www.influxdata.com/time-series-platform/telegraf/
[4]: https://www.influxdata.com/
[5]: https://www.docker.com/
[6]: https://www.speedtest.net/apps/cli/
[8]: https://blog.hypriot.com/
[9]: https://github.com/influxdata/telegraf/blob/master/plugins/inputs/exec/
[10]: telegraf/telegraf.conf
[11]: .env
[12]: https://github.com/influxdata/telegraf/blob/master/plugins/outputs/influxdb/
[13]: https://github.com/timokluser-dev
[14]: https://github.com/Bedasek
[15]: https://github.com/raaaimund/internet-speed-monitor/pull/7
[16]: https://github.com/raaaimund/internet-speed-monitor/issues/9
