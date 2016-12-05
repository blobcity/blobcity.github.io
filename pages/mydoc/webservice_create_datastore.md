---
title: Saving or updating a record
sidebar: mydoc_sidebar
permalink: webservice-create-datastore.html
folder: mydoc
---

## Create Datastore

```
{
  "username" : "root",
  "password" : "root",
  "q" : "create-ds",
  "p" : {
    "name" : "datastore1"
  }
}
```

This simple request creates a datastore if another datastore with the same name is not already present. The ds parameter is used as the name of the datastore that will be created.

The user must have the necessary permission to create a datastore for this operation to succeed. If you are using BlobCity on a multi-tenant cloud environment, then this option will not be available to you. You will have to use the BlobCity database management portal to create the datastore.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000
}
```

The response acknowledges creation of the datastore. If creation fails an `ack` value of `0` is returned along with the cause that allows further diagnosis of the error.
{% include links.html %}
