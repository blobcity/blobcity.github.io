---
title: View Cluster
sidebar: mydoc_sidebar
permalink: cli-view-cluster.html
folder: mydoc
---

## View Cluster

```
blobcity>view-cluster
```

Provides a layout of the cluster that includes the node-id, ip address, online status and current load factor of all nodes. The command returns the list of all nodes that are registered with the cluster irrespective of whether they are currently online or offline.

**Response Structure**

```
{
    "nodes" : [
     {
       "node-id" : "1",
       "ip" : "192.168.0.101",
       "status" : "online",
       "load" : 0.8
     }, 
     {
       "node-id" : "2",
       "ip" : "192.168.0.102",
       "status" : "offline"
     } 
    ]
}
```

The details of the nodes are collected into a JSONArray mapped to the key `nodes` in the response. Each element of the JSONArray is a JSONObject that represents in a single node. The parameters of the JSONObject are explained in the below table.

| Parameter | Description |
|-----------|-------------|
| node-id | Unique identifier of the node |
| ip | The IP address of the node |
| status | One of `online`, `offline`, `syncing`, `shutting` <br/><br/>An `online` status indicates that the node is active, connected to the cluster and fully working<br/><br/>An `offline` status indicates that the node is powered down or disconnected form the cluster, but definitely not reachable for any operations.<br/><br/>A `syncing` status indicates that the nodes is performing a first time connect or reconnection to the cluster and data sync is in progress. On successful sync operation the status will change to online. <br/><br/>A `shutting` status indicates that a graceful power down command has been fired up on the node, and the node is currently executing the shutdown.|
| load | Reported only for `online` nodes. Indicates the current load factor of the node as value in the range of 0 to 1 with 1 being a heavily loaded node.|
{% include links.html %}
