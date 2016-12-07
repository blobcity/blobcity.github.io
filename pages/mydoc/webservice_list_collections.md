---
title: List Collections
sidebar: mydoc_sidebar
permalink: webservice-list-collections.html
folder: mydoc
---

## List Collections

```
{
  "username" : "root",
  "password" : "root",
  "q" : "list-collections"
  "p" : {
    "ds" : "datastore1"
  }
}
```

Fetches the list of collections present within the specified data store. The list of collections returned will be only the ones that the connecting user has access to. A success response is expected if the user does not have access to any collections within the datastore, but has access to the datastore. An error response is expected if the query is fired on a datastore to which the user does not have access.

The name of the datastore is specified by the `ds` parameter in the payload.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "c" : ["datastore1.collection1", "datastore1.collection2"]
  }
}
```

The response contains the list of collections accessible to the connecting user within the specified datastore. The collections are returned as a JSONArray of String’s placed within the `c` element in the response payload. Each collection name appears in the format `datastoreName.collectionName`.
{% include links.html %}
