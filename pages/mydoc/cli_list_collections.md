---
title: List Collections
sidebar: mydoc_sidebar
permalink: cli-list-collections.html
folder: mydoc
---

## List Collections

```
blobcity>list-collections {ds}
```

Fetches the list of collections present within a specified datastore. The name of the datastore is specified by the `{ds}` parameter. The list of collections returned will be only the ones that the connecting user has access to. A success response is expected if the user does not have access to any collections within the datastore, but has access to the datastore. An error response is expected if the query is fired on a datastore to which the user does not have access.

For sake of maintaining query conventions, the name of each collection appears in the format `datastoreName.collectionName`
{% include links.html %}
