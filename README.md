# Apache Pinot Tutorial
 
Apache Pinot is a realtime distributed analytics datastore, that provides ultra low-latency and high throughput analytics. It can ingest data from offline data sources (such as Hadoop and flat files) as well as streaming events (such as Kafka). Pinot was build at LinkedIn, and is now the defacto analytics engine at LinkedIn for both site facing as well as internal use cases. Pinot powers analytics at a lot of other companies such as Uber, Slack, Weibo, 7-11 and many more.
To find out more about Apache Pinot and the community, visit [Apache Pinot](https://pinot.apache.org/).

This repo contains sample files used in the [Apache Pinot Tutorial video](). All the commands used in the video can be found below in the ** How to setup a Pinot cluster ** section below. 

## How to setup a Pinot cluster
All the commands used in the video are listed below. 

### Prerequisites
1. Java 8 or higher
2. Apache Maven https://maven.apache.org/index.html

### Getting Pinot

Download the latest release from [Apache Pinot Downloads](https://pinot.apache.org/download/)

```
# make a directory for the tutorial
cd
mkdir pinot_tutorial
cd pinot_tutorial
cp ~/Downloads/apache-pinot-incubating-0.3.0-bin.tar.gz .
tar -zxvf apache-pinot-incubating-0.3.0-bin.tar.gz
cd apache-pinot-incubating-0.3.0-bin
```

### Start Zookeeper

```
bin/pinot-admin.sh StartZookeeper -zkPort 2181
```

** Install Zooinspector **

```
# Download
git clone https://github.com/zzhang5/zooinspector.git
cd zooinspector/

# Build
mvn clean package

# Run
chmod +x target/zooinspector-pkg/bin/zooinspector.sh
target/zooinspector-pkg/bin/zooinspector.sh

# Connect to localhost:2181
```

### Start Controller

** Controller 1 **
```
bin/pinot-admin.sh StartController -zkAddress localhost:2181 -clusterName PinotCluster -controllerHost 9001
```

** Controller 2 **
```
bin/pinot-admin.sh StartController -zkAddress localhost:2181 -clusterName PinotCluster -controllerHost 9002
```

### Start Broker

** Broker 1 **
```
bin/pinot-admin.sh StartBroker -zkAddress localhost:2181 -clusterName PinotCluster -brokerPort 7001
```

** Broker 2 **
```
bin/pinot-admin.sh StartBroker -zkAddress localhost:2181 -clusterName PinotCluster -brokerPort 7002
```

### StartServer

** Server 1 **
```
bin/pinot-admin.sh StartServer -zkAddress localhost:2181 -clusterName PinotCluster -serverPort 8001 -serverAdminPort 8011
```

** Server 2 **
```
bin/pinot-admin.sh StartServer -zkAddress localhost:2181 -clusterName PinotCluster -serverPort 8002 -serverAdminPort 8012
```

The cluster is set up! Explore the cluster using Zooinspector. Explore the Admin endpoints using Rest API on the controller localhost:9001

Check out any of the example folders for steps on how to push data into the cluster.








