# Elasticsearch basics

## Documents

JSON data, every document has unique id.

## Indices

an index powers search into all documents within a collection types.

they contain **<ins>inverted indices</ins>** that let you search across everything within them at once and mappings that define schema for the data within.

- **inverted indices**  
  quickly map search terms to documents

Ex:

| words  | occurs in              |
| ------ | ---------------------- |
| word 1 | document 1, document 2 |
| word 2 | document 1             |
| word 3 | document 1, document 2 |

## TF-IDF

**Term frequency \* Inverse document frequency**

- **Term frequency**  
  how often term appears in given document.

- **Document frequency**  
  how often term appears in all documents.

- **TF/DF**  
  relevance of term in a document.

## Using Indices

- RESTful API
- Client API
- Analytic Tools - Kibana

## How elastoc search scales

Index is split into shards

- documents are hashed to a particular shard
- Each shard may be on a different node on a cluster
- Every shard is a self contained <ins>**Lucene**</ins> index of its own

## Primary and replica shards

application round robins requests amongst nodes.

- **Node**  
  install of elasticsearch. usually 1 per physical server.

write request routed to primary shard then replicated.  
read request routed to any shard.

Elasticsearch manages redundancy makes it fault tolerant.  
odd number of nodes a food idea.

<ins>Number of primary shards can not be changed later</ins>

can add more replicas for read throughput.

**worst case -** need to reindex data

number of shards set up front via `PUT`

`number_of_replicas` as per primary shard.
