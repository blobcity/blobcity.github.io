---
title: Apply License
sidebar: mydoc_sidebar
permalink: cli-apply-license.html
folder: mydoc
---

## Load Code

```
blobcity>apply-license {node-id} {license}
```

Applies the specified license to the specified node. The node is specified by its node-id as specified by the `{node-id}` parameter and the license to apply to the node is specified by the `{license}` parameter. A node with the specified {node-id} needs to be registered in the cluster and currently active and reachable for the license to be applied. The license key provided should be a valid encrypted licensed issued by BlobCity corresponding to the `{node-id}`. BlobCity issues a license key per `{node-id}`, so a valid license that is generated for a different `{node-id}` will not work.

The operation requires the connecting user to have a `manage-license` permission. The applied license will override any existing license applied on the node.

This operation is not permitted in the hosted cloud deployments of the database.
{% include links.html %}
