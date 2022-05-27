# Elastic Search Basics
- "An index" a "Search engine" a "Analytic database"? Short answer yes...long answer...
- Originated from a simple search-engine to help with Shay Bannons wife's cooking recipies.

## What is Elastic Search
- At its core, you can think of Elasticsearch as a server that can process JSON requests and give you back JSON data.

- distributed, open-source search and analytics engine built on **Apache Lucene** and developed in **Java**. 
- Started as a scalable version of the Lucene open-source search framework then added the ability to horizontally scale Lucene indices.
- It's able to achieve fast search responses because instead of searching the text directly, it searches an index.

- It uses a structure based on documents instead of tables and schemas and come with extensive REST APIs for storing and searching the data.


# Logical Concepts
## Documents
- are the basic unit of information that can be indexed in Elastisearch expressed in JSON, which is the global internet data interchange format.
- Think of a document like a row in a relational database, representing a given entity.
- A document can be more than just text, it can be any structured data encoded in JSON. 
- Each Document has a unique ID and a given data type, which describes what kind of entity the document is. 

## Indices
- An index is a collection of documents that have similar characteristics. An index is the highest level entity that you can query against in Elasticsearch. 
- you can think of an index as being similar to a database in a relational database schema. 
- Any documents in an index are typically logically related. 

## Inverted Index
- An index in Elasticsearch is actually what's called an inverted index, which is the mechanism by which all search engines work.
- It is a data structure that stores a mapping from content. such as words or numbers, to its locations in a document or a set of documents. 
- Basically, it is a hashmap-like data structure that directs you from a word to a document. 
- An inverted index doesn't store strings directly and instead splits each document up to individual search terms then maps each search term to the documents those search terms occur within. 

# Backend Components
## Cluster
- is a group of one or more node instances that are connected together. 
- The power of a cluster lies in the distribution of tasks, searching, and indexing, across all the nodes in the cluster

## Node
- A node is a single server that is a part of a cluster. A node stores data and participates in the cluster's indexing and search capabilities. 
- configurations include: 
  - **Master Node** controls the search cluster and is responsible for all cluster-wide operations like creating/deleting an index and adding/removing nodes
  - **Data Node** Stores data and executes data-related operations such as search and aggregation
  - **Client Node** Forwards cluster requests to the master node and data-related requests to data nodes

## Shards
- search provides the ability to subdivide the index into multiple pieces called shards.
- each shard is in itself a fully-functional and independent "index" that can be hosted on any node within a cluster.
- By distributing the documents in an index across multiple shards, and distributing those shards across multiple nodes. Elastic search can ensure redundancy, which both protects against hardware failures and increases query capacity as nodes are added to a cluster.

## Replicas
- search allows you to make one or more copies of your index's shards which are called "replica shards" or just "replicas". 
- replica shard is a copy of a primary shard. each document in an index belongs to one primary shard
- Replicas provide redundant copies of your data to protect against hardware failure and increase capacity to serve read requests like searching or retrieving a document


# Kibana
- is a data visualization and management tool for Elasticsearch that provides real-time histograms, line graphs, pie charts, and maps. 
- it lets you visualize your elastic search data and navigate the Elastic Stack. 
- Major drawback is that every visualization can only work against a single index/index pattern. 

# Logstash
- is used to aggregate and process data and send it to Elasticsearch. It is an open-source, server-side data processing pipeline that ingests data from a multitude of sources simultaneously, transforms it and then sends it to collect.
- It also transforms and prepares data regardless of format by identifying named fields to build structure, and transform them to converge on a common format. 

# Beats
- is a collection of lightweight, single purpose data shipping agents used to send data from hundreds or thousands of machines and systems to Logstash or Elasticsearch. 
- Beats are great for gathering data as they can sit on your servers, with your containers, or deploy as functions then centralize data in search. 
- e.g filebeat can sit on your server, monitor log files as they come in, parses them, and import into elasticsear h in near-real-time