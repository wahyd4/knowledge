# Elasticsearch

Elasticsearch is a search engine based on the Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents.


## Tips

## Calculate number of replicas

> N >= R + 1

N : number of nodes
R: Number of replicas

### How to resolve unassigned shards

https://www.datadoghq.com/blog/elasticsearch-unassigned-shards/#reason-3-you-need-to-reenable-shard-allocation
