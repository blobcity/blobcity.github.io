---
title: Truncate Collection
sidebar: mydoc_sidebar
permalink: cli-truncate-collection.html
folder: mydoc
---

## Truncate Collection

```
blobcity>truncate-collection {ds}.{collection}
```

The operation results in truncating the specified collection. The name of the datastore is specified by the `{ds}` parameter, and the name of the collection is specified by the `{collection}` parameter. All data within the collection will be deleted by the operation. The operation does not affect schema of the collection. The truncate collection operation is expected to return a success response when fired on a already truncated collection.

Based on the configuration of your installation, the data of the truncated collection can be restored using the `undo-truncate-collection` command.

{% include links.html %}
