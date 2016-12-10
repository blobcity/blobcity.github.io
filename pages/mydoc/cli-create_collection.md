---
title: Create Collection
sidebar: mydoc_sidebar
permalink: cli-create-collection.html
folder: mydoc
---

## Create Collection

```
blobcity>create-collection {ds}.{collection} {storage-type}
```

Creates a new collection within the specified datastore. The datastore within which the collection is to be created is specified by the `{ds}` parameter. The collection name is specified by the `{collection}` parameter. The `{storage-type}` parameter allows for specifying the storage type for the collection. The storage type can be one off `in-memory`, `on-disk` and `in-memory-non-durable` or `in-memory-nd`.

The created collection does not do any data replication in a cluster environment. This means that any data stored in the collection, will have a single copy saved on a single node. This will result in the cluster coming to a halt if any of the nodes in the cluster fails. To ensure high availability, it is recommended that when using BlobCity in a clustered environment you enable replication, as explained below.

**Creating a collection with data replication**

```
blobcity>create-collection {ds}.{collection} {storage-type} distributed {replication-factor}
```

This creates a collection where the data is distributed. The replication factor determines the number of copies of data that you want to store. The `{replication-factor}` needs to be an integer number greater than or equal to zero. There is virtually no limited to the number of replicas you can set, but for all practical reasons, more than 4 should never be required.

A `replication-factor` of 1 would indicate that one replica copy is stored. So this means that any data that is inserted into the cluster, the cluster will maintain two copies of the data. One the primary copy and another replica copy. Similarly a `replication-factor` of 2 would mean that one primary and two replica copies would be saved, so a total of 3 copies of each record would be saved in the cluster.

The `replication-factor` configuration is specific to the collection, and does not apply to every collection. The high availability possible with the cluster will be determined by the collection that maintains the least number of replication copies.

**Creating a fully mirrored collection**

```
blobcity>create-collection {ds}.{collection} {storage-type} mirrored
```

The query request creates a table with replication type of `mirrored`. Each record interred into the cluster will be saved on all nodes on the cluster. Note that there is no `replication-factor` parameter for a `mirrored` type collection, as all data in the collection is always replicated across all nodes in the cluster. The replication is consistent with new nodes that are added to a cluster on a mirrored collection with existing data.

Such collections are useful for making joins distributable. The smaller on the two tables on which you are running a join is recommended to be configured with a replication type of `mirrored` instead of `distributed`. This allows the join between the two tables to execute in a fully distributed manner, thereby allowing you to take advantage of the complete compute capabilities of the cluster for running join queries.
{% include links.html %}
