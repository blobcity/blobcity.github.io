---
title: Stop Watch Service
sidebar: mydoc_sidebar
permalink: cli-stop-watch-service.html
folder: mydoc
---

## Stop Watch Service

```
blobcity>stop-watch {location} {ds}.{collection}
```

The above command is used to stop an already running watch service. The `{location}`, `{ds}` and `{collection}` parameters should be exactly same as what were used for starting the watch service.

The command returns a success if it results in a running watching service being stopped or no watch service was running on the specified location. The command returns an error if the collection specified is invalid or not accessible to the logged in user.

If an interpreter was used to start the watch service, the same does not have to be specified during stopping of the service.
{% include links.html %}
