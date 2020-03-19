# Uploading sample data to Pinot

## Batch
 
Set BASE_DIR
```
BASE_DIR=`pwd`
```

Upload table config and schema
```
bin/pinot-admin.sh AddTable \
  -tableConfigFile $BASE_DIR/transcript-table-offline.json \
  -schemaFile $BASE_DIR/transcript-schema.json \
  -controllerPort 9001 \
  -exec
```

Upload data
```
bin/pinot-admin.sh LaunchDataIngestionJob \
    -jobSpecFile $BASE_DIR/batch-job-spec.yml
```

Explore the data using Query Console on the controller localhost:9001

## Streaming

Start Kafka
```
bin/pinot-admin.sh  StartKafka -zkAddress=localhost:2181/kafka -port 9876
```

Download latest release of Apache Kafka from [Downloads](https://kafka.apache.org/quickstart#quickstart_download)
Untar it

Create a topic
```
bin/kafka-topics.sh --create --bootstrap-server localhost:9876 --replication-factor 1 --partitions 2 --topic transcript-topic
```

Upload the realtime table config and schema
```
bin/pinot-admin.sh AddTable \
    -schemaFile /tmp/pinot-quick-start/transcript-schema.json \
    -tableConfigFile /tmp/pinot-quick-start/transcript-table-realtime.json \
    -controllerPort 9001 \   
    -exec
```

The realtime table begins to ingest from the Kafka topic immediately. Let's publish some events to the kafka topic
```
bin/kafka-console-producer.sh \
    --broker-list localhost:9876 \
    --topic transcript-topic < $BASE_DIR/rawData/transcript.json
```

The  data should arrive into the transcript table. Explore the data using Zooinspector and Query Console



