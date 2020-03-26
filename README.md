# Apache Pinot Tutorial
 
Apache Pinot is a real-time OLAP data store that can provide ultra low latency even at high throughput. It can ingest data from batch data sources such as Hadoop, S3, Azure and Google cloud storage or from streaming data sources such as Kafka, EventHub, Kinesis.

Originally built at LinkedIn, Pinot can power a variety of analytical applications such as 
* Real-time Dashboarding applications like Superset,
* Anomaly detection applications such as ThirdEye,
* Rich interactive user facing analytics Data Products such as Company Analytics, Who Viewed My Profile, UberEats Restaurant Analytics, and many more.

Pinot is also used at companies Uber, Microsoft, Weibo, Factual, Slack, and many more

This repo contains sample files used in the tutorial video [How to setup a Pinot cluster](https://www.youtube.com/watch?v=cNnwMF0pOJ8). All the commands used in the video can be found below. 

## How to setup a Pinot cluster
In the tutorial, we will setup a Pinot cluster with the following components
* 1 zookeeper
* 2 controllers
* 2 brokers
* 2 servers
Once the cluster is up and running, we see how to load data into Pinot and query it.
At the end, we show how Pinot is resilient to failures.

Below are listed all commands used in the tutorial video. 

### Prerequisites
Before we get started, make sure to go over this list of prerequisites

| No. | Step | Link | 
| ----| ---- |------| 
| 1 | Download sample data and configs | <https://github.com/npawar/pinot-tutorial> | 
| 2 | Download latest Pinot release binary | <https://pinot.apache.org> |
| 3 | Install Java 9 or higher | <https://openjdk.java.net> |
| 4 | Install Apache Maven 3.5.0 or higher | <https://maven.apache.org> |
| 5 | Setup Zooinspector | <https://github.com/zzhang5/zooinspector> |
| 6 | Download Apache Kafka binary 2.4 or higher | <https://kafka.apache.org> |


### Start Zookeeper
Using the launcher script in `apache-pinot-incubating-0.3.0-bin` directory form the Pinot release

```
bin/pinot-admin.sh StartZookeeper -zkPort 2181
```

### Start Controller
Using the launcher script in `apache-pinot-incubating-0.3.0-bin` directory form the Pinot release

**Controller 1**
```
bin/pinot-admin.sh StartController \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -controllerPort 9001
```

**Controller 2**
```
bin/pinot-admin.sh StartController \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -controllerPort 9002
```

### Start Broker
Using the launcher script in `apache-pinot-incubating-0.3.0-bin` directory form the Pinot release

**Broker 1**
```
bin/pinot-admin.sh StartBroker \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -brokerPort 7001
```

**Broker 2**
```
bin/pinot-admin.sh StartBroker \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -brokerPort 7002
```

### StartServer
Using the launcher script in `apache-pinot-incubating-0.3.0-bin` directory form the Pinot release

**Server 1**
```
bin/pinot-admin.sh StartServer \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -serverPort 8001 -serverAdminPort 8011
```

**Server 2**
```
bin/pinot-admin.sh StartServer \
  -zkAddress localhost:2181 \
  -clusterName PinotCluster \
  -serverPort 8002 -serverAdminPort 8012
```

The cluster is set up! Explore the cluster using Zooinspector. Explore the Admin endpoints using Rest API on the controller [http://localhost:9001](http://localhost:9001).

Check out the README in transcript example folder for steps on how to push data into the cluster.








