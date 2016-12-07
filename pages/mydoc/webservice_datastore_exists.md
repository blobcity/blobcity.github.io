---
title: Datastore Exists
sidebar: mydoc_sidebar
permalink: webservice-datastore-exists.html
folder: mydoc
---

## Datastore Exists

```
{
  "username" : "root",
  "password" : "root",
  "q" : "ds-exists",
  "p" : {
    "ds" : "datastore1",
  }
}
```

Checks if the specified datastore datastore1 is present within the database. The user is required to have access to that datastore or all datastores for the operation to succeed. Users on a multi-tenant hosted instance of BlobCity have permission to only check existence of the datastore to which they have access.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "exists" : true
  }
}
```

A value of `true` for the `exists` key in the response payload indicates that the checked datastore is present in the database. A `false` value is returned if the datastore is absent or the user does not have access to the specified datastore. A `false` value hence does not confirm in-existence of the datastore. An `ack = 0` response is expected if the user does not have the permission to run the query altogether.
{% include links.html %}
