---
title: View License
sidebar: mydoc_sidebar
permalink: webservice-view-license.html
folder: mydoc
---

## View License

```
{
  "username" : "root",
  "password" : "root",
  "q" : "view-license"
}
```

Fetches license details for all nodes registered in the cluster. The details include the license type, expiry date and list of features that the license permits that are over and above the free version of the database.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "nodes" : [
      {
        "node-id" : "1",
        "ip": "192.168.0.101",
        "license-type" : "enterprise",
        "licensed-till" : "01/01/2017 00:00 GMT",
        "license-features" : ["geo-dist-data-rep", "geo-index",
          "ts-index"]
      },
      {
        "node-id" : "2",
        "ip": "192.168.0.102",
        "license-type" : "enterprise",
        "licensed-till" : "01/01/2017 00:00 GMT",
        "license-features" : ["geo-dist-data-rep", "geo-index","ts-index"]
      }
    ] 
  }
}
```

The license information is returned within the `nodes` attribute in the response payload as a JSONArray of JSONObject’s. Each element of JSONArray contains license information of a single node registered in the cluster. The license information of a registered node is returned even if the node is not currently online or connected to the cluster.

Each JSONObject contains the attributes as mentioned in the table below:

Attribute | Description
----------|-------------|
node-id | The unique identification id of the node
ip | The current IP address of the node. This is skipped if the node is not currently active
license-type | The type of license procured
licensed-till | The date of expiry of the nodes license
license-features | The features activated as part of the license

## View License of a Single Node

```
{
  "username" : "root",
  "password" : "root",
  "q" : "view-license",
  "p" : {
    "node-id" : "nnn"
  }
}
```

By specifying an explicit `node-id` in the request, the license of a single node can be viewed. The response format remains exactly the same, except for the response to contain a single entry in the JSONArray.
{% include links.html %}
