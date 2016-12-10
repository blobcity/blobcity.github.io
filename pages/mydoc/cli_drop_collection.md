---
title: Drop Collection
sidebar: mydoc_sidebar
permalink: cli-drop-collection.html
folder: mydoc
---

## Drop Collection

```
blobcity>drop-collection {ds}.{collection}
```

Drops a collection with the specified name inside the specified datastore. The name of datastore is specified by the `{ds}` parameter, and the name of the collection is specified with the `{collection}` parameter. The specified datastore must be existent for the operation to succeed. The operation results in a success response if a collection was present and was successfully deleted; or if the specified collection was in-existent and the query resulted in a no operation.

Based on the configuration of your installation, a dropped collection can be restored using the `restore-collection` command.
{% include links.html %}
