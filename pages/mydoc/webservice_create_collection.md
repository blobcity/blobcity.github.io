---
title: Saving or updating a record
sidebar: mydoc_sidebar
permalink: webservice-create-collection.html
folder: mydoc
---

## Create Collection

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory"
  }
}
```

Creates a new collection within the specified data store. The collection name is specified by the `name` parameter in the payload. The `type` parameter in the payload allows for specifying the storage type for the collection. The storage type can be one off `in-memory`, `on-disk` and `in-memory-non-durable` or `in-memory-nd`. The type parameter is optional and if none is specified it defaults to `in-memory`.

**Specifying a replication type**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory",
    "replication-type" : "distributed",
    "replication-factor" : 2
  } 
}
```

When no `replication-type` is specified the table is created with a default `replication-type` of distributed, with `replication-factor` set to `2`. This means the data in the collection will be sharded when the database is running as a cluster, and 2 copies of each data point will be stored across nodes in the cluster over and above one original copy. So 3 copies of the same record will be present at all times in a healthy cluster. The above request does exactly same as the request without the `replication-type` specified, but can be used if another replication strategy is to be supported, or a different `replication-factor` is required.

The supported replication factors are distributed and mirrored. The distributed replication factor does data sharding, while maintaining the specified number of backup copies of each data record. The mirrored replication strategy on the other hand, makes sure that all data points are present on all nodes in the cluster. The mirrored strategy is good for small tables, master tables and the smaller of two tables that are part of a distributed join query.

**Creating a mirrored type collection**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory",
    "replication-type" : "mirrored"
  }
}
```

The query request creates a table with replication-type of mirrored. Note that there is no replication-factor parameter for a mirrored type collection, as all data in the
collection is always replicated across all nodes in the cluster. The replication is consistent with new nodes that are added to a cluster on a mirrored collection with existing data.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000
}
```

Provides a simple acknowledgement indicating whether the collection was created or not.
{% include links.html %}
