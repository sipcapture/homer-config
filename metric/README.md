
## About
With following kamailio configuration files you are able to send metrics to Elasticsearch, Graylog and InfluxDB. 
You may asking yourself why we choose this approach despite the fact that homer already has some kind of metrics 
(methods, responses, kpi's) plus rudimentary alerting and the possibility to graph them. First of all the former 
solution stores all the metrics inside Mysql or Postgres. Both are great Databases but there are better solutions 
to store timeseries data in an most efficient way. The same applies to the former alerting solution. While it can 
be used for very basic scenarios like sending an E-Mail when different kinds of thresholds exceeded it's simply 
not flexible and powerfull enough to rely on it. Last but not least the homer team spend a lot of time to provide 
some kind of dashboards to graph the metrics from the internal database or graph some metrics from external sources.
Time which could be spend to provide you the ability to capture a larger range of protocols and show you the 
correlation between them. Or simply spoken to improve the core aspects of homer without trying to reinvent the wheel.

### Structure
The main entry point is the kamailio.cfg. From here you can configure:

* Parameters for Homer
* Parameters for Elasticsearch, Graylog, InfluxDB
* Choose the functions you need. In the form of uncommenting them
* Easily integrate your own functions

For example if you want to send every 1 second kpi, geo and xrtp metrics to InfluxDB.

```bash

/* Parameters for InfluxDB */
#!substdef "!INFLUXDB_HTTP_URL!http://192.168.2.1:8086!g"
#!substdef "!INFLUXDB_DB!homer!g"
#!substdef "!INFLUXDB_PRECISION!u!g"
#!substdef "!INFLUXDB_RETENTION!autogen!g"


/* Parameters for the rtimer module. How often (seconds) stats will be send. */
#!substdef "!CHECK_STATS_INTERVAL!1!g"


##!define   DO_ELASTICSEARCH
##!define   DO_GRAYLOG
#!define    DO_INFLUXDB
#!define    DO_GEO
##!define   DO_ISUP
#!define    DO_KPI
##!define   DO_MALICIOUS
##!define   DO_METHOD
##!define   DO_RESPONSE
##!define   DO_RTCPXR
##!define   DO_USERAGENT
##!define   DO_XHTTP
#!define    DO_XRTP

...

```


### Getting Started

To install homer with these configuration files you can use the homer-installer from the 
kamailio-5.x-metric branch.

```bash
git clone https://github.com/sipcapture/homer-installer.git -b kamailio-5.x-metric
cd homer-installer
./homer_installer.sh
```

The fastest way to get a Elasticsearch, Graylog or InfluxDB playground is docker.

[Elasticsearch+Kibana](https://hub.docker.com/r/nshou/elasticsearch-kibana)

[Graylog](https://hub.docker.com/r/graylog2/server)

[InfluxDB](https://github.com/influxdata/TICK-docker/tree/master/1.2)




