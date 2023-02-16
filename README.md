# Intro

This repo contains containerlab-based labs demonstrating how logs from SR Linux network elements can be collected, parsed, and stored using [Splunk](https://www.splunk.com/) with [Splunk-Connect-4-Syslog](https://splunkbase.splunk.com/app/4740) (using a [custom log parser](./app-syslog-nokia_srlinux.conf))

A series of blog posts go into the details of various deployment models:

1. [SR Linux logging with Splunk][srk-with-splunk-post] - an introduction to the modern logging infrastructure using Splunk.

## Lab Topology

The [srl-splunk.clab.yml](srl-splunk.clab.yml) topology represents a 2-tier Clos fabric with 2 clients participating in a single L2 EVPN domain.

![Splunk lab topology][topology]

Naming conventions are straighforward:

* leaf[1-3] - leaves
* spine[1,2] - spines
* client[1,2] - emulated clients

client1 connectivity uses a single interface attached to leaf1.
client2 is connected as A/S to leaf2 and leaf3 with standby link signalling using LACP.

spine1 and spine2 are acting as BGP RR. This setup is sufficient to demonstrate a way to integrate a fabric with Splunk.

## Quick start

In order to bring up your lab follow the next simple steps:

1. Clone repo

```sh
git clone https://github.com/srl-labs/srl-splunk-lab.git
cd srl-splunk-lab
```

2. Deploy the lab

```sh
cd <lab folder>
sudo clab deploy
```

## Looking at logs

Your pre-configured Splunk instance should be available via [http://localhost:8000](http://localhost:8000).
Now you can login to the dashboard (admin/changeme), go to the 'Search' tab and search for 'index="netops"'

![splunk search][screenshot]

[srk-with-splunk-post]: https://learn.srlinux.dev/blog/2023/sr-linux-logging-with-splunk/
[topology]: ./splunk_topology.png
[screenshot]: ./splunk_search.png
