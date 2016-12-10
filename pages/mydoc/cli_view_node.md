---
title: View Node
sidebar: mydoc_sidebar
permalink: cli-view-node.html
folder: mydoc
---

## View Node

```
blobcity>view-node
```

Provides details of the node on which the query is run. The query can be run on a standalone single instance of BlobCity or on a cluster. If the query is fired on a cluster, the query will return with details of the node on which the query was received. This operation is restricted for hosted cloud instances of BlobCity.

## View Another Node

```
blobcity>view-node {node-id}
```

Gets the details of the node with the specified `{node-id}`. The query can be run from any node on a cluster. The specified `{node-id}` however must be a valid node connected to the same cluster for the query to succeed.

**Response Structure**

```
{
   "node-id" : "xxx",
   "ip" : "192.168.0.101",
   "cpu" : 8,
   "mem-free" : 100000,
   "mem-total" : 1000000,
   "disk-free" : 100000,
   "disk-total" : 100000,
   "load-factor" : 0.8,
   "license-type" : "enterprise"
   "licensed-till" : "01/01/2017 00:00 GMT"
}
```

The response contains details about the node. Check the clustering section for more information on the details that are tracked per node. A brief description of each returned parameter is provided in the table below.

| Parameter | Details |
|-----------|---------|
| node-id  | The universally unique node identifier. Details returned are for the node identified by this node-id  |
| ip  | The network IP address of the node. If the node has multiple ethernet cards, this is the IP of the ethernet card that the node is connected to  |
| cpu  | The number of processor cores, with hyper-threading connected on the node  |
| mem-free  | The amount of free memory as of now in bytes  |
| mem-total  | The amount of total RAM memory available on the system in bytes  |
| disk-free  | The amount of free disk space as of now in bytes  |
| disk-total  | The amount of total disk space available on the system in bytes  |
| load-factor | A BlobCity produced load factor indicating current loading of the node. Value is in the range of 0 - 1 with a value of 1 indicating an extremely loaded node  |
| license-type  | The type of license applied on the node  |
| licensed-till  | The date till which the current license is valid  |
{% include links.html %}
