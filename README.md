# Using Sensu to monitor SNMP devices at scale

This repository contains a minimal example of using a Sensu check to monitor SNMP devices. In order to make use of the example, you'll need:

* A workstation with Docker installed
* Familiarity with Docker
* Familiarity with Sensu

The goal here isn't to provide a complete soup to nuts example, but rather to give you the resources you need to implement the patter we lay out in our blog post about monitoring SNMP devices with Sensu.

The project also relies on the use of [Prometheus' SNMP exporter][prom-snmp] to collect metrics from SNMP devices and provide an endpoint for Sensu to scrape.

## Getting started

To create a quick demo using this repository, do the following:

```
git clone https://github.com/sensu/snmp-demo.git
cd snmp-demo/docker
```

```
docker-compose up -d
```

At this point you should have a running set of containers containing a Sensu backend, a Sensu agent, two instances of the snmp container and an instance of the SNMP exporter.

## Adding Sensu resources

From the root directory of this repo, `cd` into the `sensu` directory:

```
cd sensu
```

Ensure that you have `sensuctl` downloaded and configured on your workstation. If you need to know how to do that, head over to the [Sensu Docs site][docs-sensuctl] for instructions on installing and configurin the command line utility.

Now create the two resources:

```
sensuctl create -f proxy_entities.yml
sensuctl create -f scrap_snmp.yml
```

From there, you should see two proxy entities, snmpsim and snmpsim2:

```
sensuctl entity list
```

[prom-snmp]: https://github.com/prometheus/snmp_exporter
[docs-sensuctl]: