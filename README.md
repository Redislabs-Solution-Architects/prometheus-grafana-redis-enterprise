# Pull Redis Enterprise data using Prometheus and Grafana

Basically a repo that sets this up: https://docs.redislabs.com/latest/rs/administering/monitoring-metrics/prometheus-integration/

I was mainly using with David's rl-docker so if you are not wanting to use with that then you will need to tweak some of the settings.

## Start / Stop
Standard docker-compose start command
`docker-compose up`

or... if you plan on just leaving it up for a while...

`docker-compose up &> log.out &`

currently *log.out* is in the gitignore... but whatever filename you want, just don't push it back to the repo ;-)

To stop run the standard docker-compose command..
`docker-compose stop`

## Docker network
I was using this with David's rl-docker setup which creates a docker network called 'rs-net' ... you can comment out that section of the docker-compose.yml if that is not needed... or update it to what works for you.

If you just want to create the network...

```docker network create rs-net```

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

Name it whatever you want.  Select 'Prometheus' from the drop down and enter 'http://prometheus:9090' in the address.  

Detailed instructions in step 3 here: https://docs.redislabs.com/latest/rs/administering/monitoring-metrics/prometheus-integration/


## Manage Dashboard
In UI hover over dashboard symbol and click 'manage'

click import button

paste JSON from file/s included in this folder e.g.:

`redis-enterprise-cluster-dashboard.json`

then click load, then on the next screen import... repeat for each file

See the all the pretty things...
