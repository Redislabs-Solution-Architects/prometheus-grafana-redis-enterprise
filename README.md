# Pull Redis Enterprise data using Prometheus and Grafana

## Startup
`docker-compose up`

or... if you plan on just leaving it up for a while...

`docker-compose up &> log.out &`

## Update redis host ip
The prometheus.yml contains a target for one of the internal docker IPs where RS is running.  You may need to change this to match the IP of your master node.

In this case it is connecting to a local docker IP.

```
    static_configs:
      - targets: ["172.1.0.2:8070"]
```
Prometheus config reference: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#scrape_config

## Login to grafana UI:
http://localhost:3000/

username: admin
pwd: secret

Password can be changed in the docker-compose.yml


## Add Data Sources
Click add data source.

Add Prometheus with the internal docker network IP of the prometheus server... 

change 'Access' to browser and leave default http://localhost:9090 or ... leave as server and find the prometheus docker IP endpoint

## Manage Dashboard
In UI hover over dashboard symbol and click 'manage'

click import button

paste JSON from file/s included in this folder e.g.:

`redis-enterprise-cluster-dashboard.json`

then click load, then on the next screen import... repeat for each file

See the all the pretty things...
