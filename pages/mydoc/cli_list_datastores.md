---
title: List Datastores
sidebar: mydoc_sidebar
permalink: cli-list-datastores.html
folder: mydoc
---

## List Datastores

```
blobcity>list-ds
```

Operation gets the names of all datastores present in the database cluster. The connecting user needs to be authorised to run this command.

In case of private installations, the query will return the datastore that the connecting user executing the query has access to. If the cluster has 3 datastores, but the connecting user has access to only 2 datastores, the operation will return only 2 datastores in the response. On the cloud, the query will return the datastores that the connecting user has access to.

In case the connecting user has access to no datastores, the response will be empty.
{% include links.html %}
