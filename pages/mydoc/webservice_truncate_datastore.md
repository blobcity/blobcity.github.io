---
title: Truncate Datastore
sidebar: mydoc_sidebar
permalink: webservice-truncate-datastore.html
folder: mydoc
---

## Truncate Datastore

```
{
  "username" : "root",
  "password" : "root",
  "q" : "truncate-ds",
  "p" : {
    "name" : "datastore1"
  }
}
```

The operation truncates the specified datastore. The truncation will result in data in all collections within the specified datastore to be deleted. The operation is equivalent to independently truncating each collection with the datastore. No schema of any collection within the datastore or structure of the datastore is affected by this operation. The operation is a success as long as at the end of the operation, no collection with the specified datastore has a single record. A success response is expected on requesting a truncate datastore operation on an already truncated datastore.

For cloud users all data deleted by this operation will be stored for a period of 7 days. An `undo-truncate-ds` operation can be used to undo this operation. The `undo-truncate-collection` operation can be used to undo delete of a single collection after a `truncate-ds`. For private deployments the storage of the deleted data depends on individual configurations.

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

Provides a simple success acknowledgement, if at the end of the operation no collection within the datastore has any records.

The `arch-code` can be used in future to undo the truncate operation. The same can be fetched in future by using the `list-archive` command.
{% include links.html %}
