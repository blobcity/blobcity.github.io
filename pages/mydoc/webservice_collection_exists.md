---
title: Collection Exists
sidebar: mydoc_sidebar
permalink: webservice-collection-exists.html
folder: mydoc
---

## Collection Exists

```
{
  "username" : "root",
  "password" : "root",
  "q" : "collection-exists",
  "p" : {
    "ds" : "datastore1",
    "c" : "collection1"
  }
}
```

Checks if the collection `datastore1.collection1` is present in the database. The user needs to be authorised to access the specified datastore for executing this operation. Access to the specified collection is not required.

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

A value of `true` for the `exists` key in the response payload indicates that the checked collection is present within the datastore. A value of `false` confirms that the collection is not existent.
{% include links.html %}
