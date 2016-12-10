---
title: Drop Datastore
sidebar: mydoc_sidebar
permalink: cli-drop-datastore.html
folder: mydoc
---

## Drop Datastore

```
blobcity>drop-ds {ds}
```

The query drops the specified datastore if present. The name of the datastore to drop is specified by the `{ds}` parameter. On successful execution of the request, the datastore with the specified name is guaranteed to be inexistent on the database cluster. The query is expected to return a success response even if the datastore with the specified name was in-existent when the query was fired.

Based on the configuration of your installation, a dropped datastore can be restored using the `restore-ds` command.
{% include links.html %}
