---
title: Truncate Datastore
sidebar: mydoc_sidebar
permalink: cli-truncate-datastore.html
folder: mydoc
---

## Truncate Datastore

```
blobcity>truncate-ds {ds}
```

The operation truncates the specified datastore. The name of the datastore to truncate is specified by the `{ds}` parameter.

The truncation will result in data in all collections within the specified datastore to be deleted. The operation is equivalent to independently truncating each collection with the datastore. No schema of any collection within the datastore or structure of the datastore is affected by this operation. The operation is a success as long as at the end of the operation, no collection with the specified datastore has a single record. A success response is expected on requesting a truncate datastore operation on an already truncated datastore.

For cloud users all data deleted by this operation will be stored for a period of 7 days. An `undo-truncate-ds` operation can be used to undo this operation. The `undo-truncate-collection` operation can be used to undo delete of a single collection after a `truncate-ds`. For private deployments the storage of the deleted data depends on individual configurations.
{% include links.html %}
