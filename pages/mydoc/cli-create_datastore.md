---
title: Create Datastore
sidebar: mydoc_sidebar
permalink: cli-create-datastore.html
folder: mydoc
---

## Create Datastore

```
blobcity>create-ds {ds}
```

This simple request creates a datastore if another datastore with the same name is not already present. The `{ds}` parameter is used as the name of the datastore that will be created.

The user must have the necessary permission to create a datastore for this operation to succeed. If you are using BlobCity on a multi-tenant cloud environment, then this option will not be available to you. You will have to use the BlobCity database management portal to create the datastore.

The command will respond with details of success or failure of the operation.
{% include links.html %}
