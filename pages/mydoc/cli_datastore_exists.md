---
title: Datastore Exists
sidebar: mydoc_sidebar
permalink: cli-list-datastores.html
folder: mydoc
---

## Datastore Exists

```
blobcity>ds-exists {ds}
```

Checks if the specified datastore is present within the database. The name of the datastore to check is specified by the `{ds}` parameter. The user is required to have access to that datastore or all datastores for the operation to succeed. Users on a multi-tenant hosted instance of BlobCity have permission to only check existence of the datastore to which they have access.

The response confirms to the user whether the datastore is present or not. If the user does not have access to the specified datastore, but the datastore is present, the command will confirm to the user that the datastore is absent. Thereby the command does not confirm the in-existence of the datastore, unless the logged in user is confirmed to have access to the datastore should it have been present.
{% include links.html %}
