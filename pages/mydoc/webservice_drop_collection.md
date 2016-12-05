---
title: Drop Collection
sidebar: mydoc_sidebar
permalink: webservice-drop-collection.html
folder: mydoc
---

## Drop Collection

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "drop-collection",
  "p" : {
    "name" : "collection1"
  }
}
```

Drops a collection with the specified name inside the specified datastore. The specified datastore must be existent for the operation to succeed. The operation results in a success response if a collection was present and was successfully deleted; or if the specified collection was in-existent and the query resulted in a no operation.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "arch-code" : "xxx"
  }
}
```

Provides a simple success acknowledgement, if at the end of the operation a collection with the specified name does not exist inside the specified datastore.

The `arch-code` is a unique identifier that uniquely identifies the collection archive post a successful drop operation. The code can be used in future to restore a dropped collection. It is not important to save this code at the end of the operation, as the same can be fetched in the future by using the `list-archives` command.
{% include links.html %}
