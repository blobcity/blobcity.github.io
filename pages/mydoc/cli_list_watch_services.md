---
title: List Watch Services
sidebar: mydoc_sidebar
permalink: cli-list-watch-services.html
folder: mydoc
---

## List Watch Services

```
blobcity>list-watch-services
```

The command lists all the watch services running on the node on which the command is executed. If any watch service is register on a collection to which the logged in user does not have access, then the same will be omitted from the response.

```
blobcity>list-watch-services {ds}
```

An overloaded command allows for viewing the watch services running on all collections within the specified datastore only. The name of the datastore is specified by the `{ds}` parameter. If the user does not have access to a specific collection within the datastore then watch services registered on that data store will be omitted from the response.

```
blobcity>list-watch-services {ds}.{collection}
```

An additional overloaded command allows for viewing of watch services running on an individual collection. The name of the datastore is specified by the `{ds}` parameter and the name of the collection is specified by the `{collection}` parameter. If the user does not have access to the collection, or the collection is in-existent, the command will return an error response.

{% include links.html %}
