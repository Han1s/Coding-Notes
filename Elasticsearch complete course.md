# Notes for Work

- JDBC driver should be a client library to process elastic requests
- Ideally the application should only do queries and not modify any data. That should be handled by Logstash
- for full-text searches text data types have to be stored as text and not keywords
- when closing index is unacceptable what you can do is create new index with the updated settings and use index alias for the translation
- can perhaps disable indexing for fields that wont be searched
- perhaps switch context from query to filter in some areas of the queries

# INTRODUCTION

## Introduction to the course

- Link to GitHub: https://github.com/codingexplained/complete-guide-to-elasticsearch

## Introduction to Elasticsearch

- Analytics & Full-text search engine
  - You can save events to ElasticSearch (Aggregations)
  - Use Machine Learning for predicting future data
  - Anomality detection
- **Data is stored as documents** (like rows in MySQL)
- **document contains fields** (Columns)
- **Document is a json**
- **REST API to query document**
- **Queries also in JSON**
- ES Written in JAVA
- Most popular search engine

## Overview of the Elastic Stack

- related technologies
- **ElasticSearch**
  - Contains data
- **Kibana**
  - Analytics and visualization platform
  - dashboard where you can create visualization
  - Also handles some parts as authentication etc
  - kinda web interface to the data stored in elasticsearch
  - Also like an analytics tool
- **Logstash**
  - Process logs and send them to application
  - Data processing pipeline - data are handled as events, and then shipped off to other parts.
  - consists of **inputs, filters, outputs**, each stage consists of plugin
- **X-Pack**
  - pack of features adding functionalities to ES and Kibana
    - Security (authentication, authorization)
    - Monitor performance
    - Exporting data
    - Enables Kibana to do Machine Learning
- **Graph**
  - Relationship between data (such as music algorithms and stuff - popular, relevant....)
  - Relevance capabilities to determine what is related and what is not.
- **Elasticsearch SQL**
  - query language
  - we query ES with **query DSL**
  - for developers coming from SQL you can send SQL queries. ES translates it to **DSL**.
  - Good starting point, eventually you might switch to DSL
- **Beats**
  - Data shippers
  - Agents that you install that then send data to logstash or ES
  - Different kinds do different things. 
    - Filebeat takes care of logs for example.
    - Metricbeat collects system level metrics

## Walkthrough of common architectures

- you can use client libraries for processing requests (**JDBC driver for example**)
- you should duplicate the data (mySQL and ES)
- Kibana to see interface of ES
- Metricbeat to monitor system usage, send the data to ES ingest node. We can visualize the data with Kibana
- Filebeat processes logs and stores within ES ready for analysis with Kibana. FB has modules for this to handle logs.
- Logstash processes events.
- Ideally the application should only do queries and not modify any data. That should be handled by Logstash

# GETTING STARTED

## Installing options

- Cloud solution: https://info.elastic.co/elasticsearch-service-trial-course.html?ultron=udemy-bo&blade=cpl&hulk=web&gambit=guide-to-es

## Install ElasticSearch

- after installation go to install dir and run **bin/elasticsearch**
- elastic will be available at the **port 9200**
- can try with `curl http://localhost:9200`

## Install Kibana

- after installation go to install dir and run bin/kibana
- kibana will be available at the **port 5601**
- to test go to **localhost:5601**

## Basic Architecture

- **Node is instance of ES** that stored data
- We can run as many nodes as we want
- This way we can store data on multiple machines 
- Each node belongs to a **cluster** that is a collection  of related nodes
- We can have many clusters but one is usually enough. They are completely independent by default
- You might run multiple clusters that serve multiple purposes
- When a node starts up it will either join existing cluster or create its own
- Each unit of data is called **document**
- When you **index** a document the original JSON you sent is stored together with some ES metadata
- Documents are organized via **Indices** 
- **Index** groups data together logically. Its a collection of documents that have similar characteristics. (e.g. people, departments, etc). Index can contain as many documents as you want.
- **Search queries** are run against **indices**

## Inspecting the cluster

- In **Kabana dev tools**
- `GET /_cluster/health`gets health of the cluster
- `GET /_cat/nodes?v` includes header with description
- `GET /_cat/indices?v` show indices

## Sending queries with cURL

- in the **dev tools** we can click on the query and copy it as **cURL** to transfer it to terminal command

## Sharding and Scalability

- **Sharding** is a way to divide index into a separate pieces (shard)
- The main purpose is to horizontally scale the data volume
- Each **shard** is kind of **independent** and you can think of it as a separate **index** on its own
- A shard can store two billion documents 
- An index by default contains one shard
- **Split API** increases the number of shards
- **Shard API** reduces the number of shards
- Adding shards at the beginning is easier.
- 5 shards if you expect millions of documents is a good number

## Understanding Replication

- What happens if nodes hard drive fails?
- ES supports replication of shards
- ES does it automatically
- Replications works by creating copies of shards.  They are complete copy.
- So Index contains shards which contain replica shards.
- Replication group contains the primary shard and its replicas
- Replica shards are never stored at the same node as their primary shard.
- Replication only makes sense for multiple nodes.
- As a rule of thumb replicate once, for critical data twice atleast.
- ES also supports taking **snapshots** - kind of backups. Either at index level or cluster level.
- **Replication** works with **live data**
- **Replica shards** **can serve different search requests simultaneously.** This increases the amount of requests that can be ehandled at a time.
- **ES automatically selects a shard for a given query**

## Adding more nodes to the cluster

- To scale ES, we need to add nodes
- When doing so, replica shards are also assigned.
- Typically you would download ES for each node and set it up.

## Node roles

- **Master role** is a cluster master node
  - responsible for cluster wide actions. (creating and deleting indices, ...)
  - Several nodes with this role - one will get elected as master
  - useful to ensure that cluster is stable
- **Data role **
  - enables to store data
  - search queries
  - used as part of configuring a dedicated master node
- **Ingest**
  - runs **ingest pipelines**
  - **ingesting** is adding a document to index
  - simplified **logstash pipeline** basically
  - useful for simple data transformations
- **Machine learning**
  - `node.ml` identifies node as a machine learning node
  - `xpack.ml.enabled`toggles machine learning API for the node
  - useful for running ML jobs
- **Coordination**
  - distribution of queries and the aggregation of results
  - useful for coordination-only nodes (for large clusters)
  - configured by disabling all other roles
- **Voting-only**
  - almost never used
  - participates to vote for the new master, cannot be elected though.

- When to change node roles?
  - useful for large cluster
  - Typically done when optimizing and scaling
  - but you will often change the other things first (num of nodes, shards, replicas, etc)
  - better understand what HW resources are used for
  - only change the roles if you know what you are doing

# MANAGING DOCUMENTS

## Creating & Deleting indices

- **Deleting index**
  - `DELETE /pages`
- **Creating and index**
  - `PUT /products`

## Indexing documents

```json
// Id is automatically generated
POST /products/_doc
{
  "name": "Coffee Maker",
  "price": 64,
  "in_stock": 10
}

// Creates with a custom id 
PUT /products/_doc/100
{
  "name": "Toaster",
  "price": 49,
  "in_stock": 4
}
```

- Indexes by default are created automatically

## Retrieving documents by ID

```json
GET /products/_doc/100
```

## Updating documents

```json
// used for both updating and adding new fields
POST /products/_update/100
{
  "doc": {
    "tags": ["electronics"]
  }
}
```

- documents are **immutable**
- We actually replaced the document
- The API retrieves document, changes fields and reindexes the document, replacing it.

## Scripted updates

```json
// reduces the value by one
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock--"
  }
}

// set the value to ten
POST /products/_update/100
// ctx = context
// source = source
{
  "script": {
    "source": "ctx._source.in_stock = 10"
  }
}


// use params and set the value to the value of the param quantity
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock -= params.quantity",
    "params": {
      "quantity": 4
    }
  }
}
```

## Upserts

- conditionally update or insert the document based on whether it exists
- if it exists the script is run otherwise it is indexed

```jsx
POST /products/_update/101
{
  "script": {
    "source": "ctx._source.in_stock++"
  },
  "upsert": {
    "name": "Blender",
    "price": 399,
    "in_stock": 5
  }
}
```

## Replacing documents

```json
PUT /products/_doc/100
{
  "name": "Toaster",
  "price": 71,
  "in_stock": 4
}
```

## Deleting documents

```json
DELETE /products/_doc/101
```

## Understanding Routing

- how does elastic know where to find the document? On which shard?
- `shard_num = hash (_routing) % num_primary_shards` is the formula elastic uses
- routing is completely transparent
- its possible to change the default routing
- The default strategy ensures the documents are distributed evenly

## How ES Reads Data

- coordinating node tells us where the document is stored
- resolves to a replication group
- a shard is chosen from replication group (which gives the best performance)
- the coordinating node then selects the request to the shard

## How writing data works

- Coordination node
- finds a replication group
- request go to primary shards. This shard validates the request and field values.
- The shard then performs the operation locally and forwards it to replicas.
- Operation will succeed even if it cannot be replicated to replica shards.
- **Primary terms and sequence numbers**
  - PT are a way to distinguish between old and new primary shards
  - Essentially a counter for how many times the primary shard has changed
  - sequence number is also given to each operations.
  - The primary shard increases the sequence number.
  - Enable ES to order write operations
  - These enable the ES to recover from operations where something fails.
  - For large index this is really expensive.
  - To speed up elastic has **checkpoints**
    - these are esentially sequence numbers for each replication group and replica shards.

## Understanding document versioning

- ES versions the documents we index in a very simple way
- only stores the most recent version of the document 
- store **_version** metadata field. It starts at 1 and is incremented when modifying.
- When deleting, it stores the version for 60 seconds. If we then put new document with the same id, the version will be incremented by one, otherwise it will start at 1.
- There is also **external versioning**
  - when you maintain version outside of ES, such as DBs.
  - it enables to tell you how many times doc has been modified.
  - It was previously the way t o do optimistic concurrency control.
- Now there is a better way though.
- Mostly used for legacy.

## Optimistic concurrency control

- prevent overwriting documents due to concurrent operations
- e.g. handling concurrent versions of web applications. (e.g. different threads)
- How to handle failures?
  - Retrieve document again,
  - Use new primary_term and seq_no

```json
// avoids concurrency issues. Only updates if the document has not been updated since retrieval.
POST /products/_update/100?if_primary_term=1&if_seq_no=13
{
  "doc": {
    "in_stock": 123
  }
}
```

## Update by query

- update multiple documents
- Similar to `update where` query
- first snapshot is created
- Search query is then sent to each shard
- if t he requests fails, all the operations until that point will still apply

```json
POST /products/_update_by_query
{
  // if concurrent conflict found, proceed
  "conflicts": "proceed", 
  "script": {
    "source": "ctx._source.in_stock--"
  },
  "query": {
    "match_all": {}
  }
}
```

## Delete by query

```json
POST /products/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

## Batch Processing

```json
POST /_bulk
// we are specifying the action and what index we are targeting
{ "index": { "_index": "products", "_id": 200 } }
{ "name": "Espresso Machine", "price": 199, "in_stock": 5 }
{ "create": { "_index": "products", "_id": 201 }}
{ "name": "Milk Frother", "price": 149, "in_stock": 14}

// index is specified within the request
POST /products/_bulk
{ "update": { "_id": 201 } }
{ "doc": { "price": 129 } }
{ "delete": { "_id": 200 } }
```

- To use **Bulk API**
  - the content-type must be **application/x-ndjson**
  - **application/json** is accepted, but not correct
  - Console handles it for us
  - Console tool handles it for us
- Each line **must** end with a newline character `\n` (even the last line)
  - in a text editor this means the last line should be empty
- If a single action fails, this will **not** affect the other actions
- **When** to use BULK api?
  - when importing data or modifying lots of data
  - more efficient than individual write requests

## Import data with cURL

- `curl -H "Content-Type: application/x-ndjson" -XPOST http://localhost:9200/products/_bulk --data-binary "@products-bulk.json"`

# MAPPING & ANALYSIS

## Introduction to analysis

- sometimes referred as **text analysis**
- applicable to text fields/values
- the **_source** object is not used when searching for documents
  - text is processed when the value is stored
  - **Character filter**
    - adds, removes or changes characters
    - Analyzer contains zero or more filters
  - **Tokenizers**
    - analyzer contains **one** tokenizer which splits text into tokens
    - characters may be removed as part of the tokenization
  - **Token filters**
    - receive the output of the tokenizer as input (tokens)
    - can add, remove or modify tokens
    - analyzer contains zero or more token filters
- **When ES encounters a value**:
  - `I REALLY like beer!`
    - No **character filter** applied by default
    - output: `I REALLY like beer!`
      - **Tokenizer**:
      - breaks values into tokens `I REALLY like beer!` and removes punctionation
      - output: `['I', 'REALLY', 'like', 'beer']`
        - **Token filter** lowercase
        - input: `['I', 'REALLY', 'like', 'beer']`
        - output: `['i', 'really', 'like', 'beer']`

## Using Analyze API

```json
POST /_analyze
{
  "text": "2 guys walk into     a bar, but the third... DUCKS! :-)",
  "analyzer": "standard"
}

// explicitely the same thing
POST /_analyze
{
  "text": "2 guys walk into     a bar, but the third... DUCKS! :-)",
  "char_filter": [],
  "tokenizer": "standard",
  "filter": ["lowercase"]
}
```

## Understanding Inverted Indices

- a fields values are stored in one of several data structures
  - the structure depends on the fields data type
- handled by **Apache Lucene**
- **Inverted indices** is mapping between terms and which documents contain them
  - **terms** are the tokens basically
    - `2 guys went into a bar` => 	Tokens: `['2', 'guys', 'went', 'into', 'a', 'bar']`
    - **inverted index** is created for each name/value field
  - fields with different data types use different data structures

## Introduction to mapping

- **mapping** defines the structure of documents and how they are stored
- basically a **table schema** in a db
- **explicit mapping** 
  - we define ourselves when creating an index
- **dynamic mapping**
  - elastic does automatically
  - these two can be mixed

## Overview of Data Types

- object
  - can be nested
  - is represented by `properties` key 
  - lucene does not support objects so the objects are flattened using dotation inside elastic
- nested
  - similar to object but maintains object relationship
  - enables us to query objects independently
  - must use `nested` query
- integer
- keyword
  - used for exact matching values
  - **for full-text searches use `text` datatype instead**
  - used for sorting / filtering / aggregations
- long
- boolean
- text
- double
- short
- date
- float
- ...

## How the `keyword` datatype works

- keyword fields are analyzed with the keyword analyzer
- its a no-op analyzer
  - it outputs the unmodified string as a single token
- keyword fields are used for exact matching, aggregations, sorting

## Understanding type coercion

- data types are inspected when indexing documents
- they are validated, and some values are rejected
- elastic does not use coercion when creating field mapping, **always use correct value type otherwise it will not be searched correctly!**

## Understanding arrays

- There is no such thing as an `array` data type
- Any field may contain zero or more values
  - no configuiration or mapping needed
  - simply supply an array when indexing
- **Array values should be of the same data type!**
- You can mix them if they can be coerced and coercion is enabled
- coercion is only supported if mapping is already created
- mixed datatypes are only allowed when mapping is created

## Adding explicit mappings

```json
PUT /reviews 
{
  "mappings": {
    "properties": {
      "rating": { "type": "float" },
      "content": { "type": "text" },
      "product_id": { "type": "integer" },
      "author": { 
        "properties": {
          "first_name": {"type": "text" },
          "last_name": { "type": "text" },
          "email": { "type": "keyword" }
        }
      }
    }
  }
}

// create document
PUT /reviews/_doc/1
{
  "rating": 5.0,
  "content": "Outstanding course! Bo really taught me a lot about Elasticsearch!",
  "product_id": 123,
  "author": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "johndoe123@example.com"
  }
}
```

## Retrieving mappings

```json
// mapping of the entire index
GET /reviews/_mapping

// mapping of the single field
GET /reviews/_mapping/field/content

// mapping of the object property
GET /reviews/_mapping/field/author.email
```

## Using dot notation in field names

instead of this:

```json
PUT /reviews 
{
  "mappings": {
    "properties": {
      "rating": { "type": "float" },
      "content": { "type": "text" },
      "product_id": { "type": "integer" },
      "author": { 
        "properties": {
          "first_name": {"type": "text" },
          "last_name": { "type": "text" },
          "email": { "type": "keyword" }
        }
      }
    }
  }
}
```

you can map objects like this:

```json
PUT /reviews_dot_notation
{
  "mappings": {
    "properties": {
      "rating": { "type" :"float" },
      "content": { "type": "text" },
      "product_id": { "type": "integer" },
      "author.first_name": { "type": "text" },
      "author.last_name": { "type": "text" },
      "author.email": { "type": "keyword" }
    }
  }
}
```

This can also be used with search queries

## Adding mappings to existing indexes

```json
PUT /reviews/_mapping
{
  "properties": {
    "created_at": {
      "type": "date"
    }
  }
}
```

adds mapping of that particular type to the existing index

## How does date work in ES

- specified in three ways
  - specially formatted strings
  - milliseconds since epoch (long)
  - seconds since the epoch (integer)
- Epoch refers to the 1.1.1970
- custom formats are supported
- By default:
  - 1 of 3 formats expected
    - date without time
    - date with time
    - ms since epoch
    - (UTC timezone unless specified)
    - ISO 8601 format
- How date fields are stored
  - internally as milliseconds since epoch
  - any valid value is converted to a long value internally
  - dates are converted to the UTC timezone
  - the same conversion happens for search queries

```json
PUT /reviews/_doc/2
{
  "rating": 4.5,
  "content": "Not bad. Not bad at all!",
  "product_id": 123,
  "created_at": "2015-03-27",
  "author": {
    "first_name": "Average",
    "last_name": "Joe",
    "email": "avgjoe@example.com"
  }
}

PUT /reviews/_doc/3
{
  "rating": 3.5,
  "content": "Could be better",
  "product_id": 123,
  "created_at": "2015-04-15T13:07:41Z",
  "author": {
    "first_name": "Spencer",
    "last_name": "Pearson",
    "email": "spearson@example.com"
  }
}

PUT /reviews/_doc/4
{
  "rating": 5.0,
  "content": "Incredible!",
  "product_id": 123,
  "created_at": "2015-01-28T09:21:51+01:00",
  "author": {
    "first_name": "Adam",
    "last_name": "Jones",
    "email": "adam.jones@example.com"
  }
}

PUT /reviews/_doc/5
{
  "rating": 4.5,
  "content": "Very useful",
  "product_id": 123,
  "created_at": 1436011284000,
  "author": {
    "first_name": "Taylor",
    "last_name": "West",
    "email": "twest@example.com"
  }
}

GET /reviews/_search
{
  "query": {
    "match_all": {}
  }
}
```

The dates are stored how you supplied them however

## How missing fields are handled

- all fields are optional
- you can leave out a field when indexing
- unlike relational DB when you need to allow null values
- Some integrity checks need to be done at the application level
  - e.g. having required fields
- adding a field mapping does not make a field required
- searching automatically handles missing fields (skips them out)

## Overview of mapping parameters

- most important parameters

- this is not exhaustive

  - most of them rare or advanced

- **format** spoecifies date format fiels. Use default whenever possible.

  - `strict_date_optional_time||epoch_millis`
  - using Java's `DateFormatter` syntax
    - `dd/MM/yyyy`
  - using built-in formats
    - `epoch_seconds`

- **properties**

  - defines nested fields for object and nested fields 
  - ` "properties": { "name" : { "type": " text" } }`

- **coerce**

  - enable or disable coercion of values

  - ```json
    PUT /sales
    {
        "mappings": {
            "properties": {
                "amount": {
                    "type": "float",
                    "coerce": false
                }
            }
        }
    }
    ```

  - ```json
    // On INDEX level
    PUT /sales
    {
        "settings": {
            "index.mapping.coerce": false
        },
        "mappings": {
            "properties": {
                "amount": {
                    "type": "float",
                    // here you can overwrite coercion
                    "coerce": true,
                }
            }
        }
    }
    ```

- **doc_values**

  - advanced parameter

  - ES makes use of several data structures

  - no single data structure serves all purposes

    - inverted indices are good for searching but not for other use cases

  - doc values is used by apache Lucene optimized for different data access patterns

  - its opposite of inverted index

  - used for sorting, aggregations, scripting

  - its an addition, not replacement of inverted indexes

  - set the `doc_values` parameter to `false` to save disk space

  - storing data in multiple data structures multiples data.

  - also slightly increases indexing speed

  - disable if you wont use aggregations, sorting, scripting

  - cannot changed without reindexing documents into new index

    - use with caution, and try to anticipate how you will query data

  - ```json
    PUT /sales
    {
        "mappings": {
            "properties": {
                "buyer_email": {
                    "type": "keywords",
                    "doc_values": false
                }
            }
        }
    }
    ```

- **norms**

  - normalization factors used for relevance scoring

  - often we dont just want to filter results but also rank them

  - norms can be disabled to save disk space

    - useful for fields that wont be used for relevance scoring (e.g. tags field) 

  - ```json
    PUT /products
    {
        "mappings": {
            "properties": {
                "tags": {
                    "type": "text",
                    "norms": false
                }
            }
        }
    }
    ```

- **index**

  - disables indexing for a field

  - field cannot be used within search queries

  - will still be stored within `_source` just not used for searching

  - saves disk space and improves indexing throughput

  - often used for time series data

  - fields with indexing disabled can still be used for aggregation

  - ```json
    PUT /server-metrics
    {
        "mappings": {
            "properties": {
                "server_id": {
                    "type": "integer",
                    "index": false
                }
            }
        }
    }
    ```

  - **null_value**

    - NULL values cannot be indexed or searched

    - same with empty array

    - use this parameter to replace null values with another value.

    - only works for explicit NULL values

    - the value you define must be of the same data type as the field data type

    - does not affect the value stored within `_source` 

    - ```json
      PUT /sales
      {
          "mappings": {
              "properties": {
                  "partner_id": {
                      "type": "keyword",
                      "null_value": "NULL"
                  }
              }
          }
      }
      ```

  - **copy_to**

    - used to copy multiple field into a group field

    - simply specify the name of the target field as the value

    - e.g. first_name and last_name => full_name

    - values will be copied, not terms or tokens

      - the analyzer of the target field is used for the values
      - target field is not part of the _source

    - ```json
      PUT /sales
      {
          "mappings": {
              "properties": {
                  "first_name": {
                      "type": "text",
                      "copy_to": "full_name"
                  },
                  "last_name": {
                      "type": "text",
                      "copy_to": "full_name"
                  },
                  "full_name": {
                      "type": "text"
                  }
              }
          }
      }
      
      POST /sales/_doc
      {
          "first_name": "John",
          "last_name": "Doe"
      }
      ```


## Updating existing mappings

- generally you **cannot** update field mappings
- some parameters can be updated.
- field mappings **cannot** be removed
- The solution is to **reindex**

```json
// Will not work
PUT /reviews/_mapping
{
  "properties": {
    "product_id": {
      "type": "keyword"
    }
  }
}

// Will work
PUT /reviews/_mapping
{
  "properties": {
    "author": {
      "properties": {
        "email": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    }
  }
}
```

## Reindexing documents with the Reindex API

- `_source` data type does not reflect how the values are indexed
- `_source`containes the filed values supplied at index time
- its common to use `_source`values from search result
- we can modify the `_source`value when reindexing
- alternatively this can be handled at the application level

```json
// Creates mappings for new index
PUT /reviews_new
{
  "mappings" : {
    "properties" : {
      "author" : {
        "properties" : {
          "email" : {
            "type" : "keyword",
            "ignore_above" : 256
          },
          "first_name" : {
            "type" : "text"
          },
          "last_name" : {
            "type" : "text"
          }
        }
      },
      "content" : {
        "type" : "text"
      },
      "created_at" : {
        "type" : "date"
      },
      "product_id" : {
        "type" : "keyword"
      },
      "rating" : {
        "type" : "float"
      }
    }
  }
}

// Reindexes as it is
POST /_reindex
{
  "source": {
    "index": "reviews"
  },
  "dest": {
    "index": "reviews_new"
  }
}

// Reindex and covert data type
POST /_reindex
{
  "source": {
    "index": "reviews"
  },
  "dest": {
    "index": "reviews_new"
  },
  "script": {
    "source": """
      if (ctx._source.product_id != null) {
        ctx._source.product_id = ctx._source.product_id.toString();
      }
    """
  }
}
```

## Introduction to field aliases

- field names can be changed when reindexing documents
- alternative is to use `field aliases`
  - doesnt require documents to be reindexed
  - aliases can be used within queries
  - aliases are defined with a field mapping
- field alias can actually be updated (only its target field though)
- simply perform a mapping update with a new **path** value
- possible because aliases dont affect indexing
  - its a query-level construct
- ES also uses index aliases

```json
PUT /reviews/_mapping
{
  "properties": {
    "comment": {
      "type": "alias",
      "path": "content"
    }
  }
}

GET /reviews/_search
{
  "query": {
    "match": {
      "content": "outstanding"
    }
  }
}

GET /reviews/_search
{
  "query": {
    "match": {
      "comment": "outstanding"
    }
  }
}
```

## Multi-field mappings

- field can be mapped multiple ways

```json
PUT /multi_field_test
{
  "mappings": {
    "properties": {
      "description": {
        "type": "text"
      },
      "ingredients": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          }
        }
      }
    }
  }
}


POST /multi_field_test/_doc
{
  "description": "To make this spaghetti carbonara, you first need to...",
  "ingredients": ["Sphagetti", "Bacon", "Eggs"]
}

GET /multi_field_test/_search
{
  "query": {
    "match_all": {}
  }
}

GET /multi_field_test/_search
{
  "query": {
    "term": {
      "ingredients.keyword": "Sphagetti"
    }
  }
}
```

## Index Template

- specify settings and mappings
- applied to indices that match one or more patterns
- patterns may include wildcards
- **index templates** take effect when creating new indices
- a new index may match multiple **index templates**
- **index template** can be updated as well, this only affects new indices
- **index template** can be deleted and retrieved using same endpoint

```json
PUT /_template/access-logs
{
  "index_patterns": ["access-logs-*"],
  "settings": {
    "number_of_shards": 1,
    "index.mapping.coerce": false
  }, 
  "mappings": {
    "properties": {
      "@timestamp": {
        "type": "date"
      },
      "url.original": {
        "type": "keyword"
      },
      "http.request.referrer": {
        "type": "keyword"
      },
      "http.response.status_code": {
        "type": "long"
      }
    }
  }
}

PUT /access-logs-2020-01-01

GET /access-logs-2020-01-01
```

## Introduction to the Elastic Common Schema (ECS)

- ECS is a specification defining set of common fields and how they should be mapped
- before ECS there was no cohesion between field names
- ECS means that common fields are named the same
  - e.g. **@timestamp**
- documents are referred as **events**
- mostly useful for standard events (logs, metrics, etc) - this enables to use kibana without customization

## Introduction to dynamic mapping

- the first time ES encounters a field es will create a mapping for it dynamically which will be used later
- e.g.
  - **int** => **long**
  - **float** => **float**
  - **bool** => **bool**
  - **date** string => **date**
  - **object** => **ocject** of other types
  - **array** => depends on the first value that is not null
  - array of **text** => both **keyword** and **text** and **ignore** strings that are longer than 256 for **keywords**
    - (also possibly **float** or **long** if string is number, but this is disabled. Numbers should be sent as numbers)
- the larger the index the more it makes sense to create mapping

## Combining explicit and dynamic mapping

- explicit and dynamic mapping can be combined
- example

```json
PUT /people
{
  "mappings": {
    "properties": {
      "first_name": {
        "type": "text"
      }
    }
  }
}

POST /people/_doc
{
  "first_name": "Bo",
  "last_name": "Andersen"
}

GET /people/_mapping

DELETE /people
```

## Configuring dynamic mapping

```json
PUT /people
{
  "mappings": {
    "dynamic": false, # Disables dynamic mapping
    "properties": {
      "first_name": {
        "type": "text"
      }
    }
  }
}

POST /people/_doc
{
  "first_name": "Bo",
  "last_name": "Andersen"
}

# Only the first_name will be mapped
GET /people/_mapping

# will find the result
GET /people/_search
{
  "query": {
    "match": {
      "first_name": "Bo"
    }
  }
}

# will not find any matches
GET /people/_search
{
  "query": {
    "match": {
      "last_name": "Andersen"
    }
  }
}

DELETE /people
```

- the unmapped fields will be ignored
- the fields will still be parts of the **_source** however that is not what ES uses for searching
- no **inverted index** is created for unmapped fields
- not recommended behavior
- you can set dynamic to **strict**
  - ES will reject unmapped fields
  - all fields must be mapped explicitly

- **numeric detection**

  - detects whether string fields contains only float / int

  ```json
  PUT /computers
  {
     "mappings": {
         "numeric_detection": true
     }
  }
  ```

- **date detection**

  ```json
  PUT /computers
  {
      "mappings": {
          "date_detection": false
      }
  }
  ```

## Dyanmic templates

- conditional mapping

- simple example

  ```json
  PUT /dynamic_templates_test
  {
    "mappings": {
      "dynamic_templates": [
        {
          "integers": {
            "match_mapping_type": "long",
            "mapping": {
              "type": "integer"
            }
          }
        }]
    }
  }
  
  # map datatype that would be mapped as long (integers) to integer instead of long
  ```

- example is dont map strings as keywords over certain length

- we can include more than one condition for the one dynamic template

- **match** and **unmatch** parameters

  - used to specify conditions for field names
  - field name must match the condition specified by the **match** parameter
  - **unmatch** is used to exclude fields that were matched
  - both of them support **wildcards** (*****)
  - yo ucan for example state that all documents starting with **text_** string are matched only as a string and not as keyword etc.
  - good for utilizing naming conventions (can use **regex**)

- **patch match** and **patch_unmatch**

  - evalue the full field path not just the field names
  - e.g. **name.fist_name**
  - wildcards also supported

- **copy_to** can be utilized to copy the value to a different field. Therefore first_name + lsat_name can become full_name field

- **placeholders**

  - can be used in string values by enclosing them with curly braces
  - **dynamic_type**

- Difference between index templates vs dynamic templates

  - **index templates** apply mappings and index settings for matching indices
    - this happens when indices are created and their names match a pattern
  - **dynamic template** are evaluated when new fields are encountered
    - and dynamic mapping is enabled

## Mapping recommendations

- dynamic mapping is convenient, but often not good idea in production
- save disk space when optimizing mapping
- set **dynamic** to **strict** not false
  - avoids surprises and unexpected results
- dont always map string as both text and keyword unless you need to do so
  - for full text searches use text mapping
  - for aggregations, sorting, filtering exact values keyword mapping
  - if both then both
- disable coercion if you can.
  - its a way for  ES to do it wrong way
  - always use correct data types
- for whole numbers the integer data type might be enough
- long can store larger numbers but uses more disk space
- same with floats and double, usually float is enough
- parameters:
  - set **doc_values** to **false** if you dont need sorting, aggregations and scripting
  - set **norms** to false if you dont need relevance scoring
  - set **index** to false if you dont need to fo filter on values
    - you can still do aggregations
    - these parameters probably only worth when storing lots of document

## Stemming & stop words

- standard analyzer just transfers string to lowercase
- **stemming** is the process of reducing words to their root word (e.g. loved => love)
- **stop words** words that are filtered out during the analysis process (a, the, at, of, on)
  - less common in ES today than in the past, the algorithm improved signicicantly
  - stop words generally not removed

## Analyzer and search queries

- if you store a *drinking* through stemming analyser into *drink* and user then searches for *drinking* the match will still be found cause the query will run through analyser
- queries are run lowercased by default
- queries are analyzed the same way as fields are indexed - can be changed but is not recommended

## Built-in analyzers

- they can usually be configured so you can build on them

- **standard analyzer**
  - splits text at word boundaries and removes punctiation
  - done by the **standard** tokenizer
  - lowercases letters with the **lowercase** token filter
  - contains the **stop** token filter
- **simple analyzer**
  - splits into tokens when encountering anything else than letter
  - lowercases letters with the **lowercase** tokenizer
    - unusual and performance hack
- **whitespace analyzer**
  - splits text into tokens by whitespace
  - does **not** lowercase letters
- **keyword analyzer**
  - no-op - leaves the input text intact and outputs it as a single token
  - used for keywords fields by default
- **pattern analyzer**
  - regular expression is used to match token separators
  - it should match whatever should split the text into tokens
  - very flexible
  - lowercases letters but can be disabled
- **language-specific analyzers**
  - viz doc
  - usually good starting point

## Creating custom analyzers

```json
PUT /analyzer_test
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_custom_analyzer": {
          "type": "custom",
          "char_filter": ["html_strip"],
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "stop",
            "asciifolding"
          ]
        }
      }
    }
  }
}

PUT /analyzer_test
{
  "settings": {
    "analysis": {
      "filter": {
        "danish_stop": {
          "type": "stop",
          "stopwords": "_danish_"
        }
      }, 
      "analyzer": {
        "my_custom_analyzer": {
          "type": "custom",
          "char_filter": ["html_strip"],
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "danish_stop",
            "asciifolding"
          ]
        }
      }
    }
  }
}


POST /_analyze
{
  "char_filter": ["html_strip"], 
  "text": "I&apos;m in a <em>good</em> mood&nbsp;-&nbsp;and I <strong>love</strong> aca!"
}

POST /analyzer_test/_analyze
{
  "analyzer": "my_custom_analyzer", 
  "text": "I&apos;m in a <em>good</em> mood&nbsp;-&nbsp;and I <strong>love</strong> aca!"
}
```

## Adding analyzers to existing indices

- **open index** is available for indexing and search requests
- **closed index** will refuse requests
  - read and write are blocked
  - necessary for performing some operations
- **dynamic settings** can be changed without closing the index first
  - requires no downtime
- **static settings** require the index to be closed first
  - the index will be briefly unavailable
  - analysis settings are static settings

## Updating analyzers

- analyzers can be updated
- pay attention to existing documents
  - they were analyzed using the old version of the analyzer
  - reindex these documents to avoid headaches
- try to get analyzers right before indexing documents

```json
PUT /analyzer_test/_mapping
{
  "properties": {
    "description": {
      "type": "text",
      "analyzer": "my_custom_analyzer"
    }
  }
}

POST /analyzer_test/_doc
{
  "description": "Is that Peter' s cute-looking dog?"
}

GET /analyzer_test/_search
{
  "query": {
    "match": {
      "description": {
        "query": "that",
        "analyzer": "keyword"
      }
    }
  }
}

POST /analyzer_test/_close

PUT /analyzer_test/_settings
{
  "analysis": {
    "analyzer": {
      "my_custom_analyzer": {
        "type": "custom",
        "tokenizer": "standard",
        "char_filter": ["html_strip"],
        "filter": [
          "lowercase",
          "asciifolding"
        ]
      }
    }
  }
}

POST /analyzer_test/_open

GET /analyzer_test/_settings

# updates all the documents with the new analyzer
POST analyzer_test/_update_by_query?conflicts=proceed
```



# Introduction to Searching

## Search methods

- **Query DSL:**

  ```json
  GET /product/_search
  {
      "query": {
          "match": {
              "description": {
                  "value": "red wine"
              }
          }
      }
  }
  ```

- **request URI**

  ```json
  GET /product/_search?q=name:pasta
  ```

  - a bit limited
  - harder to read
  - good for quick searches when debugging or developing

## Searching with the request URI

```json
# search all
GET /products/_search

GET /products/_search?q=name:lobster

GET /products/_search?q=tags:Meat

# using boolean
GET /products/_search?q=tags:Meat AND name:Tuna
```

- using curl or similar requires **%20** for empty space
- the results are sorted by relevance, which means more relevant results are found first

## Introducing the Query DSL

- **leaf query** search for values in fields
- **compound query** compounds leaf queries or compound queries

```json
GET /product/_search 
{
    "query": {
        "match_all": {}
    }
}
```

## How searching works

- client (server) communicates with search cluster. Cluster then does matching and responses with the results.

## Understandying query results

- **took** represents number of ms to execute
- **timed_out** flag whether it timed out
- **shards** contains total searched shards and how many of them were searched successfully
- **hits** contains search results
  - **hits** contains the hits themselves. By default 10 is returned
    - **_score** indicates how well document matched query

## Understanding relevance scores

- first whether the document matches at all
- second is **_score** which the results are sorted by
  - these days **okapi BM25** is used (better at handling stop words)
    - **term frequency** how many times does the term appear in the field? The more the more relevant.
    - **inverse document frequency** how often does the term appear in the index (the more often, the lower the score)
    - **field-length norm** the longer the field the less relevance
    - can be configured
- can use **explain: true** to explain query score

## Debugging unexpected search results

- **explain API** - why given document did or did not match a query

  ```json
  GET /products/_explain/1
  {
    "query": {
      "term": {
        "name": "lobster"
      }
    }
  }
  ```

## Query contexts

- **query context** - how well do documents match the query? Relevance score is also calculated.
- **filter context** - do documents match? No relevance scores are calculated (used for filterind dates, status, range, etc.)
- if a query class should affect relevance use the query context, otherwise the filter context

## Term queries vs full-text queries

- **term query** is not analyzed at all. Search for exact values.
- **match query** is analyzed and tokenized

# Term Level Queries

## Searching for a term

```json
GET /products/_search
{
    "query": {
        "term": {
            "is_active": true
        }
    }
}
```

or

```json
GET /products/_search
{
    "query": {
        "term": {
            "is_active": {
                "value": true
            }
        }
    }
}
```

## Searching for multiple terms

```json
GET /products/_search
{
    "query": {
        "terms": {
            "tags.keyword": [
                "Soup",
                "Cake"
            ]
        }
    }
}
```

## Retrieving documents based on IDs

```json
GET /products/_search
{
    "query": {
        "ids": {
            "values": [1, 2, 3]
        }
    }
}
```

##  Matching documents with range values

```json
GET /products/_search
{
    "query": {
        "range": {
            "in_stock": {
                "gte": 1,
                "lte": 5
            }
        }
    }
}

GET /products/_search
{
    "query": {
        "range": {
            "in_stock": {
                "gte": 01-01-2010,
                "lte": 31-12-2010,
                "format": "dd-MM-yyyy"
            }
        }
    }
}
```

## Working with relatives date (date math)

```json
GET /products/_search
{
  "query": {
    "range": {
      "created": {
        "gte": "2010/01/01||-1y"
      }
    }
  }
}

GET /products/_search
{
  "query": {
    "range": {
      "created": {
        "gte": "now"
      }
    }
  }
}
```

## Matching documents with non-null values

```json
GET /products/_search
{
  "query": {
    "exists": {
      "field": "tags"
    }
  }
}
```

## Matching based of prefixes

```json
GET /products/_search
{
  "query": {
    "prefix": {
      "tags.keyword": "Vege"
    }
  }
}
```

## Searching with the wildcards

```json
GET /products/_search
{
  "query": {
    "wildcard": {
      "tags.keyword": "Veg*ble"
    }
  }
}
```

- question mark matches a single character

```json
GET /products/_search
{
  "query": {
    "wildcard": {
      "tags.keyword": "Veg???ble"
    }
  }
}
```

- **these queries might be slow, especially when placing at the beginning**

## Searching with regex

- not all regex characters are supported

```json
GET /products/_search
{
  "query": {
    "regexp": {
      "name": "[0-9]"
    }
  }
}
```

# Assignment to complete

# Full Text Queries

## Flexible matching with the match query

```json
GET /recipe/_search
{
  "query": {
    "match": {
      "title": "Recipes with pasta or spaghetti"
    }
  }
}

GET /recipe/_search
{
  "query": {
    "match": {
      "title": {
        "query": "pasta spaghetti",
        "operator": "and"
      }
    }
  }
}
```

## Matching phrases

- order matters

```json
GET /recipe/_search
{
  "query": {
    "match_phrase": {
      "title": "spaghetti Puttanesca"
    }
  }
}
```

## Searching multiple fields

```json
GET /recipe/_search
{
  "query": {
    "multi_match": {
      "query": "pasta",
      "fields": ["title", "description"]
    }
  }
}
```

# Adding Boolean Logic to Queries

- leaf queries search for value in a given category
- compound query wrap queries to create compound queries

## Querying with boolean logic

- **filter context** - whether the document matches the query
- **query context** - relevance scores are calculated

```json
GET /recipe/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "ingredients.name": "parmesan"
          }
        }
      ],
      "must_not": [
        {
          "match": {
            "ingredients.name": "tuna"
          }
        }
      ],
      "should": [
        {
          "match": {
            "ingredients.name": "parsley"
          }
        }
      ], 
      "filter": [
        {
          "range": {
            "preparation_time_minutes": {
              "lte": 15
            }
          }
        }
      ]
    }
  }
}
```

- in this context **should** is used to boost score basically
- the difference between **must** and **filter** is that **must** contributes to the relevance score while filter does not

## Debugging bool queries with named queries

```json
GET /recipe/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "ingredients.name": {
              "query": "parmesan",
              "_name": "parmesan_must"
            }
          }
        }
      ],
      "must_not": [
        {
          "match": {
            "ingredients.name": {
              "query": "tuna",
              "_name": "tuna_must_not"
            }
          }
        }
      ],
      "should": [
        {
          "match": {
            "ingredients.name": {
              "query": "parsley",
              "_name": "parsley_should"
            }
          }
        }
      ], 
      "filter": [
        {
          "range": {
            "preparation_time_minutes": {
              "lte": 15,
              "_name": "prep_time_filter"
            }
          }
        }
      ]
    }
  }
}
```

- we will see the explanation in **matched_queries**
- good to see why some document ranked higher

## How the match query works

- **match query** is basically a convenient wrapper around **bool query** that simplifies writing queries

```json
GET /recipe/_search
{
  "query": {
    "match": {
      "title": "pasta carbonara"
    }
  }
}

GET /recipe/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "title": {
              "value": "pasta"
            }
          }
        },
        {
          "term": {
            "title": {
              "value": "carbonara"
            }
          }
        }
      ]
    }
  }
}
```

- this is equal

```json
GET /recipe/_search
{
  "query": {
    "match": {
      "title": {
        "query": "pasta carbonara",
        "operator": "and"
      }
    }
  }
}

GET /recipe/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "title": {
              "value": "pasta"
            }
          }
        },
        {
          "term": {
            "title": {
              "value": "carbonara"
            }
          }
        }
      ]
    }
  }
}
```

- this is equal as well
- **bool query** is **NOT** analyzed (not lowercased)

# Joining queries

- elasticsearch support simple joins
- this is **highly inefficient though**

## Querying nested objects

- used in combination with **nested** data type

have to use nested query

```json
GET /department/_search
{
  "query": {
    "nested": {
      "path": "employees",
      "query": {
          "bool": {
          "must": [
            {
              "match": {
                "employees.position": "intern"
              }
            },
            {
              "term": {
                "employees.gender.keyword": {
                  "value": "F"
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

- more complex
- enables you to query each object independently
- harder to keep objects document

## Nested inner hits

- can be used with **join** queries as well

```json
GET /department/_search
{
  "_source": false, 
  "query": {
    "nested": {
      "path": "employees",
      "inner_hits": {}, 
      "query": {
        "bool": {
          "must": [
            {
              "match": {
                "employees.position": "intern"
              }
            },
            {
              "term": {
                "employees.gender.keyword": {
                  "value": "F"
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

## Mapping document relationships

```json
# Here we define parent - child relationship
# parent is the employee
PUT /department
{
  "mappings": {
    "properties": {
      "join_field": {
        "type": "join",
        "relations": {
          "department": "employee"
        }
      }
    }
  }
}
```

## Adding documents

```json
PUT /department/_doc/1
{
  "name": "Development",
  "join_field": "department"
}

PUT /department/_doc/1
{
  "name": "Marketing",
  "join_field": "department"
}

PUT /department/_doc/3?routing=1
{
  "name": "Bo Andersen",
  "age": 28,
  "gender": "M",
  "join_field": {
    "name": "employee",
    "parent": 1
  }
}

PUT /department/_doc/4?routing=2
{
  "name": "John Doe",
  "age": 44,
  "gender": "M",
  "join_field": {
    "name": "employee",
    "parent": 2
  }
}

PUT /department/_doc/5?routing=1
{
  "name": "James Evans",
  "age": 32,
  "gender": "M",
  "join_field": {
    "name": "employee",
    "parent": 1
  }
}
PUT /department/_doc/6?routing=1
{
  "name": "Daniel Harris",
  "age": 52,
  "gender": "M",
  "join_field": {
    "name": "employee",
    "parent": 1
  }
}
PUT /department/_doc/7?routing=2
{
  "name": "Jane Park",
  "age": 23,
  "gender": "F",
  "join_field": {
    "name": "employee",
    "parent": 2
  }
}
PUT /department/_doc/8?routing=1
{
  "name": "Christina Parker",
  "age": 29,
  "gender": "F",
  "join_field": {
    "name": "employee",
    "parent": 1
  }
}
```

## Querying by parent ID

```json
GET /department/_search
{
  "query": {
    "parent_id": {
      "type": "employee",
      "id": 2
    }
  }
}
```

## Querying child documents by parent

```json
GET /department/_search
{
  "query": {
    "has_parent": {
      "parent_type": "department", 
      "score": true,
      "query": {
        "term": {
          "name.keyword": "Development"
          }
        }
      }
    }
  }
}
```

## Querying parent by child document

- were getting parent components that have child components that have certain criteria
- we can include relevance by **score_mode**
  - **min** - the lowest score of matching child documents is mapped into the parent
  - **max** - the opposite
  - **sum** - matching children scores are summed up and mapped into the parent
  - **avg** - average score of the children is mapped into the parent
  - **none** - dont consider the relevance score at all (default)
- we can add **min_children** or **max_children**
- supports **sorting** by scripting

## Multi -level relations

```json
PUT /company
{
  "mappings": {
    "properties": {
      "join_field": {
        "type": "join",
        "relations": {
          "company": ["department", "supplier"], # company has multiple departments and suppliers
          "department": "employee" # department has multiple employees
        }
      }
    }
  }
}

PUT /company/_doc/1
{
  "name": "My Company Inc.",
  "join_field": "company"
}

PUT /company/_doc/2?routing=1
{
  "name": "Development",
  "join_field": {
    "name": "department",
    "parent": 1
  }
}

PUT /company/_doc/3?routing=1 # The routing has to refer to the most distant parent
{
  "name": "Bo Andersen",
  "join_field": {
    "name": "employee",
    "parent": 2
  }
}

PUT /company/_doc/4
{
  "name": "Another COmpany, Inc",
  "join_field": "company"
}

PUT /company/_doc/5?routing=4
{
  "name": "Marketing",
  "join_field": {
    "name": "department",
    "parent": 4
  }
}

PUT /company/_doc/6?routing=4
{
  "name": "John Doe",
  "join_field": {
    "name": "employee",
    "parent": 5
  }
}

GET /company/_search
{
  "query": {
    "has_child": {
      "type": "department",
      "query": {
        "has_child": {
          "type": "employee",
          "query": {
            "term": {
              "name.keyword": "Bo Andersen"
            }
          }
        }
      }
    }
  }
}
```

## Parent/child inner hits

```json
GET /department/_search
{
    "query": {
        "has_parent": {
            "parent_type": "department",
            "inner_hits": {},
            "query": {
                "term": {
                    "name.keyword": "Development"
                }
            }
        }
    }
}
```

## Terms lookup mechanism

- fetching terms from the document

```json
PUT /users/_doc/1
{
  "name": "John Roberts",
  "following" : [2, 3]
}

PUT /users/_doc/2
{
  "name": "Elizabeth Ross",
  "following" : []
}

PUT /users/_doc/3
{
  "name": "Jeremy Brooks",
  "following" : [1, 2]
}

PUT /users/_doc/4
{
  "name": "Diana Moore",
  "following" : [3, 1]
}

PUT /stories/_doc/1
{
  "user": 3,
  "content": "Wow look, a penguin!"
}

PUT /stories/_doc/2
{
  "user": 1,
  "content": "Just another day at the office... #coffee"
}

PUT /stories/_doc/3
{
  "user": 1,
  "content": "Making search great again! #elasticsearch #elk"
}

PUT /stories/_doc/4
{
  "user": 4,
  "content": "Had a blast today! #rollercoaster #amusementpark"
}

PUT /stories/_doc/5
{
  "user": 4,
  "content": "Yay, I just got hired as an Elasticsearch consultant - so excited!"
}

PUT /stories/_doc/6
{
  "user": 2,
  "content": "Chilling at the beach @ Greece #vacation #goodtimes"
}

GET /stories/_search
{
  "query": {
    "terms": {
      "user": {
        "index": "users",
        "id": "1",
        "path": "following"
      }
    }
  }
}
```

## Join limitations

- documents must be stored within the same index
- Parent & child documents must be on the same shard
- only one join field per index
  - join field can have multiple relationships tho
  - child relations can be added to existing parents
- document can only have one parent
- document may have multiple children

## Join field performance considerations

- using join fields is slow, avoid when possible
  - except for few cases:
- The query gets slower the more documents you add
- As the number of documents increases the time increases a lot
- each level of relation adds overhead to query
- in some scenario makes sense
  - one to many relationship between two document types where there is a lot more of one type than the other
- the nested data type is better than join
- generally you should not map relationships but store data as a structure optimized for efficient searching
- make relationships nested or as a regular fields
- unless you gave a good reason to use join fields try to denormalize your data

# Controlling Query Results

## Specifiyng the result format 

- yaml

```json
GET /recipe/_search?format=yaml
{
  "query": {
    "match": { "title": "pasta" }
  }
}
```

- pretty (for terminal)

```json
GET /recipe/_search?pretty
{
  "query": {
    "match": { "title": "pasta" }
  }
}
```

## Source filtering

- you can disable **source** to just search for ids of documents

```json
GET /recipe/_search
{
    "_source": false,
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search
{
    "_source": "created",
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search
{
    "_source": "ingredients.name",
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search
{
    "_source": "ingredients.*",
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search
{
    "_source": ["ingredients.*", "servings"],
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search
{
    "_source": {
        "includes": "ingredients.*",
        "excludes": "ingrediens.name"
    },
    "query": {
        "match": { "title": "pasta" } 
    }
}
```

## Specifying the result size

- default is 10

```json
GET /recipe/_search?size=2  // total still contains the amount of returned items
{
    "_source": false,
    "query": {
        "match": { "title": "pasta" } 
    }
}

GET /recipe/_search  // same thing
{
    "size": 2,
    "_source": false,
    "query": {
        "match": { "title": "pasta" } 
    }
}
```

## Specifying an offset

- the numbers of matches to skip before returning matches
- this is for implementing pagination

```json
GET /recipe/_search  // return 3. and 4. hit
{
    "size": 2,
    "from": 2,
    "_source": false,
    "query": {
        "match": { "title": "pasta" } 
    }
}
```

## Pagination

- **total_pages**  = ceil(total_hits / page_size)

- **from** = (page_size * (page_number) - 1)

- limited to 10 000 results

- **search_after** to results after first 10k

  - https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-body.html#request-body-search-search-after

  ```json
  GET /recipe/_search
  {
    "_source": false,
    "query": {
      "match_all": {}
    },
    "sort": [
      "preparation_time_minutes"
    ]
  }
  ```

## Sorting results

```json
// basic
GET /recipe/_search
{
  "_source": false,
  "query": {
    "match_all": {}
  },
  "sort": [
    "preparation_time_minutes"
  ]
}

// specifying desc
GET /recipe/_search
{
  "_source": false,
  "query": {
    "match_all": {}
  },
  "sort": [
    { "created": "desc" }
  ]
}

// second first and second sort order
GET /recipe/_search
{
  "_source": [ 
    "preparation_time_minutes", "created"
    ],
  "query": {
    "match_all": {}
  },
  "sort": [
    { "preparation_time_minutes": "asc" },
    { "created": "desc" }
  ]
}
```

## Sorting by multi-value fields

```json
// averages all ratings
GET /recipe/_search
{
  "_source": "ratings",
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "ratings": {
        "order": "desc",
        "mode": "avg"
      }
    }
  ]
}
```

## Filter contexts

- filters usually used for numbers and date ranges and keyword fields

```json
GET /recipe/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "pasta"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "preparation_time_minutes": {
              "lte": 15
            }
          }
        }
      ]
    }
  }
}
```

- filters are more efficient
- ES caches filters used frequently and we dont calculate relevance scores

# Aggregations

## Introduction to aggregations

- grouping and extracting statistics from your data

## Metric aggregations

- single-value numeric metric aggregations

- multi-value numeric metric aggregations

- **sum aggregation**

  ```json
  GET /order/_search
  {
    "size": 0,
    "aggs": {
      "total_sales": {
        "sum": {
          "field": "total_amount"
        }
      }
    }
  }
  ```

- **average**

  ```json
  GET /order/_search
  {
    "size": 0,
    "aggs": {
      "total_sales": {
        "sum": {
          "field": "total_amount"
        }
      },
      "avg_sale": {
        "avg": {
          "field": "total_amount"
        }
      },
      "min_sale": {
        "min": {
          "field": "total_amount"
        }
      },
    " max_sale": {
        "max": {
          "field": "total_amount"
        }
      }
    }
  }
  ```

- **cardinality**

   ```json
   // how many salesmen are associated with the sales, the number is approximate
   GET /order/_search
   {
     "size": 0,
     "aggs": {
       "total_salesmen": {
         "cardinality": {
           "field": "salesman.id"
         }
       }
     }
   }
   
   ```

- **count** - the number of values the aggregation used to do its work

- **stats**

```json
// returns count min max avg sum
GET /order/_search
{
  "size": 0,
  "aggs": {
    "amount_stats": {
      "stats": {
        "field": "total_amount"
      }
    }
  }
}
```

## Introduction to bucket aggregations

- create sets of documents
- shows how many unique values we have in the given field

```json
GET /order/_search
{
  "size": 0,
  "aggs": {
    "status_terms": {
      "terms": {
        "field": "status"
      }
    }
  }
}
```

- **sum_other_doc_count** says how many non-displayed fields there are	

```json
GET /order/_search
{
  "size": 0,
  "aggs": {
    "status_terms": {
      "terms": {
        "field": "status",
        "missing": "N/A" # Shows fields that are null or missing
        "min_doc_count": 0, # how many items to create a bucket
        "order": {
          "_key": "asc"  # ascending order by terms
      	}
      }
    }
  }
}
```

- calculated document counts are approximate. So it might not be approximate in some scenarios.

## Document counts are approximate

- because of the distributed nature (multiple shards)
- its better to keep size at 10 even if you look for 3
- this is only present if youre browsing multiple shards
- **doc_count_error_upper_bound** 
  - contains a number representing max possible number for term that was not count
  - its an error margin basically

## Nested aggregations (subaggregations)

```json
GET /order/_search
{
  "size": 0,
  "aggs": {
    "status_terms": {
      "terms": {
        "field": "status"
      },
      "aggs": {
        "status_stats": {
          "stats": {
            "field": "total_amount"
          }
        }
      }
    }
  }
}
```

- the statistics you will see will be relevant to the bucket they are in
- if you dont add query the elastic will use **match_all** query

```json
GET /order/_search
{
  "size": 0,
  "query": {
    "range": {
      "total_amount": {
        "gte": 100
      }
    }
  }, # using query context
  "aggs": {
    "status_terms": {
      "terms": {
        "field": "status"
      },
      "aggs": {
        "status_stats": {
          "stats": {
            "field": "total_amount"
          }
        }
      }
    }
  }
}
```

- aggregations added on the top level operate in the context of the query
- sub-aggregations run within the context of the bucket (parent aggregations)
- bucket aggregations can contain bucket aggregations

## Filtering out documents

```json
GET /order/_search
{
  "size": 0,
  "aggs": {
    "low_value": {
      "filter": {
        "range": {
          "total_amount": {
            "lte": 50
          }
        }
      },
      "aggs": {
        "avg_amount": {
          "avg": {
            "field": "total_amount"
          }
        }
      }
    }
  }
}
```

## Defining bucket rules with filters

```json
GET /recipe/_search
{
  "size": 0,
  "aggs": {
    "my_filter": {
      "filters": {
        "filters": {
          "pasta": {
            "match": {
              "title": "pasta"
            }
          },
          "sphagetti": {
            "match": {
              "title": "spaghetti"
            }
          }
        }
      },
      "aggs": {
        "avg_rating": {
          "avg": {
            "field": "ratings"
          }
        }
      }
    }
  }
}
```

## Range aggregations

- **range**

  ```json
  GET /order/_search
  {
    "size": 0,
    "aggs": {
      "amount_distribution": {
        "range": {
          "field": "total_amount",
          "ranges": [
            {
              "to": 50
            },
            {
              "from": 50, 
              "to": 100
            },
            {
              "from": 100
            }
          ]
        }
      }
    }
  }
  ```

  - creates 3 buckets based on ranges

- **date_range**

## Histograms

```json
GET /order/_search
{
  "size": 0,
  "query": {
    "range": {
      "total_amount": {
        "gte": 100
      }
    }
  }, 
  "aggs": {
    "amount_distribution": {
      "histogram": {
        "field": "total_amount",
        "interval": 25,
        "min_doc_count": 1, # minimum amount of hits to form a bucket (can be 0)
        "extended_bounds": { # now the boundaries will be 0 and 500
          "min": 0,
          "max": 500
        }
      }
    }
  }
}

# same but for dates
GET /order/_search
{
  "size": 0,
  "aggs": {
    "orders_over_time": {
      "date_histogram": {
        "field": "purchased_at",
        "calendar_interval": "month"
      }
    }
  }
}
```

## Global aggregations

```json
GET /order/_search
{
  "query": {
    "range": {
      "total_amount": {
        "gte": 100
      }
    }
  },
  "size": 0,
  "aggs": {
    "stats_expensive": { # uses the query context 
      "stats": {
        "field": "total_amount"
      }
    },
    "all_orders": { # does not use the query context because it is global
      "global": {},
      "aggs": {
        "stats_amount": {
          "stats": {
            "field": "total_amount"
          }
        }
      }
    }
  }
}
```

## Missing field balues

- usually used in context with other aggregations

```json
POST /order/_search
{
  "size": 0,
  "aggs": {
    "orders_without_status": {
      "missing": {
        "field": "status"
      },
      "aggs": {
        "missing_stum": {
          "sum": {
            "field": "total_amount"
          }
        }
      }
    }
  }
}
```

## Aggregated nested objects

```json
GET /department/_search
{
  "size": 0,
  "aggs": {
    "employees": {
      "nested": {
        "path": "employees"
      },
      "aggs": {
        "minimum_age": {
          "min": {
            "field": "employees.age"
          }
        }
      }
    }
  }
}
```

# Improving search results

## Proximity searches

```json
GET /proximity/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "spicy sauce",
        "slop": 2 # how many times term can be moved, so 2 is switch terms order for example
      }
    }
  }
}
```

## Affecting relevance scoring with proximity

- the closer the proximity the higher the relevance score
- TODO: not really that useful, watch the lecture if interested

## Fuzzy match query (handling typos)

- we can use **fuzziness** parameter
- fuzziness is on term basis, so for every word

```json
GET /product/_search
{
  "query": {
    "match": {
      "name": {
        "query": "l0bster",
        "fuzziness:": "auto"  // the edit distance (char edits)
      }
    }
  }
}
```

- auto means:
  - length 1-2 -> fuziness no t used
  - length 3-5 -> max edit distance is 1
  - length: >5 -> max edit distance is 2
- reduces performance
- max fuzziness should be 2. Auto is a good value to use
- transpozitions can be disabled (switching letter positions)

## Fuzy query

- term level, not full text. Its not alyzed
- you should prefer using the match query with fuzziness parameter

```json
GET /product/_search
{
  "query": {
    "fuzzy": {
      "name": {
        "value": "LOBSTER",
        "fuzziness": "auto"
      }
    }
  }
```

## Adding synonyms

```json
PUT /synonyms
{
  "settings": {
    "analysis": {
      "filter": {
        "synonym_test": {
          "type": "synonym", 
          "synonyms": [
            "awful => terrible",
            "awesome => great, super",
            "elasticsearch, logstash, kibana => elk",
            "weird, strange"
          ]
        }
      },
      "analyzer": {
        "my_analyzer": {
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "synonym_test"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "my_analyzer"
      }
    }
  }
}
```

- term level are not analyzed so dont work with synonyms

## Adding synonyms from the file

```json
PUT /synonyms
{
  "settings": {
    "analysis": {
      "filter": {
        "synonym_test": {
          "type": "synonym",
          "synonyms_path": "analysis/synonyms.txt"
        }
      },
      "analyzer": {
        "my_analyzer": {
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "synonym_test"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "my_analyzer"
      }
    }
  }
} 
```

- if you add the file later use **update_by_query** to update.

## Highlighting matches in fields

```json
GET /highlighting/_search
{
  "_source": false,
  "query": {
    "match": { "description": "Elasticsearch story" }
  },
  "highlight": {
    "fields": {
      "description" : {}
    }
  }
}
```

- to wrap with a different tag:

```json
GET /highlighting/_search
{
  "_source": false,
  "query": {
    "match": { "description": "Elasticsearch story" }
  },
  "highlight": {
    "pre_tags": [ "<strong>" ],
    "post_tags": [ "</strong>" ],
    "fields": {
      "description" : {}
    }
  }
}
```

## Stemming

```json
PUT /stemming_test
{
  "settings": {
    "analysis": {
      "filter": {
        "synonym_test": {
          "type": "synonym",
          "synonyms": [
            "firm => company",
            "love, enjoy"
          ]
        },
        "stemmer_test" : {
          "type" : "stemmer",
          "name" : "english"
        }
      },
      "analyzer": {
        "my_analyzer": {
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "synonym_test",
            "stemmer_test"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "my_analyzer"
      }
    }
  }
}
```

- adding highlight

```json
GET /stemming_test/_search
{
  "query": {
    "match": {
      "description": "enjoy work"
    }
  },
  "highlight": {
    "fields": {
      "description": {}
    }
  }
}
```

