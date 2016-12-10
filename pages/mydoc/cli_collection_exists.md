---
title: Collection Exists
sidebar: mydoc_sidebar
permalink: cli-list-datastores.html
folder: mydoc
---

## Collection Exists

```
blobcity>collection-exists {ds}.{collection}
```

Checks if the specified collection is present. The name of the datastore is specified by the `{ds}` parameter and the name of the collection is specified by the `{collection}` parameter. The user needs to be authorised to access the specified datastore for executing this operation. Access to the specified collection is not required.

If the collection is present, the query responds to the user confirming the same. The command however informs the user of the collection being absent, if the collection is actually absent, of if the user does not have permissions to access the collection. Hence a collection absent response is not a confirmation on the collection being absent, unless it is confirmed that the logged in user would have access to the collection should it have been present.
{% include links.html %}
