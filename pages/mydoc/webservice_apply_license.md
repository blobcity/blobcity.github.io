---
title: Apply License
sidebar: mydoc_sidebar
permalink: webservice-apply-license.html
folder: mydoc
---

## Apply License

```
{
  "username" : "root",
  "password" : "root",
  "q" : "apply-license",
  "p" : {
    "node-id" : "xxx",
    "license" : "zzz"
  }
}
```

Applies the specified license to the node with the specified `node-id`. A node with the specified `node-id` needs to be registered in the cluster and currently active and reachable for the license to be applied. The license key provided should be a valid encrypted licensed issued by BlobCity corresponding to the `node-id`. BlobCity issues a license key per `node-id`, so a valid license that is generated for a different `node-id` will not work.

The operation requires the connecting user to have a `manage-license` permission. The applied license will override any existing license applied on the node.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000
}
```

Provides a simple success response confirming the application of the new license. The operation is expected to return a `ack` value of `0` if the license is invalid, node id provided is invalid or the specified node could not be reached.
{% include links.html %}
