---
title: List Datastores
sidebar: mydoc_sidebar
permalink: webservice-list-datastores.html
folder: mydoc
---

## List Datastores

```
{
  "username" : "root",
  "password" : "root",
  "q" : "list-ds"
}
```

Operation gets the names of all datastores present in the database cluster. The connecting user needs to be authorised to run this command.

In case of private installations, the query will return the datastore that the connecting user executing the query has access to. If the cluster has 3 datastores, but the connecting user has access to only 2 datastores, the operation will return only 2 datastores in the response. On the cloud, the query will return the datastores that the connecting user has access to.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "ds" : ["datastore1", "datastore2"]
  }
}
```

The success responses contains the names of the datastores the connecting user has access to. The datastores are contained as a JSONArray of String’s mapped to the element ds inside the payload.

In case the connecting user has access to no datastores, the response will contain an empty JSONArray.
{% include links.html %}
