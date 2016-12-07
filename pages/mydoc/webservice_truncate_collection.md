---
title: Truncate Collection
sidebar: mydoc_sidebar
permalink: webservice-truncate-collection.html
folder: mydoc
---

## Truncate Collection

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "truncate-collection",
  "p" : {
    "name" : "collection1"
  }
}
```

The operation results in truncating the specified collection. All data within the collection will be deleted by the operation. The operation does not affect schema of the collection. The truncate collection operation is expected to return a success response when fired on a already truncated collection.

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

Provides a simple success acknowledgement, if at the end of the operation the specified collection has no records.

The `arch-code` can be used in future to undo the truncate operation. The same can be fetched in future by using the `list-archive` command.
{% include links.html %}
