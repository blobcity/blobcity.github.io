---
title: Revoke License
sidebar: mydoc_sidebar
permalink: webservice-revoke-license.html
folder: mydoc
---

## Revoke License

```
{
  "username" : "root",
  "password" : "root",
  "q" : "revoke-license",
  "p" : {
    "node-id" : "xxx"
  }
}
```

Fully revokes the license of the specified node. A node with the specified `node-id` must be a valid node in the cluster, and must be reachable for the operation to succeed. Once the license is revoked, the node will work as it worked on boot up as if the node never had a license applied to it. All capabilities and features will be downgraded to that of a free edition of the database. A new license can be applied to activate the locked features.

This command does not affect any data, even if some of the data was created with specialised features that are not available as part of the free license. It will always be possible to read all data present in all datastores and collections, but it may not be possible to operation on all data. All functionality can however be restored by applying a new license and at no point will revoking a license make the system permanently unusable.

This command does not have to be used for upgrading license, or renewing license. The apply license command can be directly used for upgrades and renewing without having to revoke an already applied license, as the apply automatically overwrites a new license.

The revoke operation also provides a revoke confirmation code. This code can be submitted to BlobCity to get a fresh license for a new node-id. This is the primary purpose for which the command is provided, so that if you desire to phase out a node, you can revoke the license and make that license available for use with another node.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "revoke-confirmation" : "xxx"
  }
}
```

Provides a success acknowledgement confirming that the license was revoked. The `revoke-confirmation` maps to a confirmation token that can be used to procure a new license for another node if the license that was revoked is still active.
{% include links.html %}
