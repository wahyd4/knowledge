# Kafka

# What is Kafka

<iframe width="560" height="315" src="https://www.youtube.com/embed/FKgi3n-FyNU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Apache Kafka is an open-source distributed event streaming platform

## How to migrate self hosted Kafka to Some hosting vendor

1. Setup target Kafka cluster
2. Setup various replicators to replicate schemas and events in kafka. Before replicate schemas, make sure the schema registry in target cluster is empty and in `IMPORT_ONLY` mode.
3. Setup users, roles for applications in the target clusters
4. Start migrate consumers including apps and sink connectors
    1. Reset consumer offset in the target Kafka cluster for a consumer(As the offsert will be different in most cases, unless the no events from the source cluster ever been deleted.)
    2. Update Kafka configurations and scema registries for the consumer to the new cluster
    3. Restarted consumer to consume events from the new cluster
5. Stop schema replicator before migrating publisher, otherwise new publisher won't be able to publish schemas as the schema registry is in IMPORT mode. Once updating target schema registry to `READ_WRITE` mode, then schema replicator won't work anymore.
6. Once all the consumers migerated, then migrated publichers (apps and source connectors)
    1. Update Kafka configurations for Kafka clusters and shema registries
    2. Restart publishers
7. Stop replcators and source Kafka clusters

## A typical Kafka workflow with schema registry

![typical workflow](https://docs.confluent.io/platform/current/_images/schema-registry-and-kafka.png)

Note: image from https://docs.confluent.io/platform/current/schema-registry/index.html


## Some facts and best practices

* Set proper partitions for topics, would be better to start with 3 or more depends on the numbers of events and type of events in the topic
* Enable RBAC for topics, which means a Kafka user/service account can only access what he supposed to access. Minimal access scope
* Use Debezium related source connnectors to achieve at least once delivery guarantee.
* Use various sink connectors to export data via Restful API/S3 bucket and so on.
* Set proper schema compatibility levels and tests to make sure existing events can be still consumed by new version of consumers.
