---
title: Start Watch Service
sidebar: mydoc_sidebar
permalink: cli-start-watch-service.html
folder: mydoc
---

## Start Watch Service

```
blobcity>start-watch {location} {ds}.{collection}
```

The command is used to make BlobCity watching a file or folder and import existing data and any new data that is written to those files. This feature is commonly used for reading log files, where you want the data written to the log files from an external program, to be automatically and immediately imported into a collection inside BlobCity.

The `{location}` should point to a folder or file on the node on which this command is run. If the location is valid the BlobCity DB will do a first time import of all data present in the files within the folder or all data of a specific file. Each file is processed line by line, and each line of each file will be imported as a separate record.

All imported data is stored inside the specified collection. The name of the datastore is specified by the `{ds}` parameter and the name of the collection within the datastore is specified by the `{collection}` parameter.

The watch service is started independently on each node, and not on all nodes of the cluster. The command needs to be run on the node on which the watch service is to be started.

Multiple watch services can be started on the same collection or on different collections. A single file or folder location can be used only once per watch service per collection. The same file or folder maybe used for another watch service started on another collection.

**Passing data through an interpreter**

```
blobcity>start-watch {location} {ds}.{collection} {interpreter-name}
```

Importing file data without an interpreter, makes the data get imported into a plain text format. This is not really usable for any advanced analytics you might want to conduct on the data. Each line of the file can be passed through an interpreter, that can interpret the data for extraction of key meta elements. The interpreter can add structure to the data, that makes the data now usable for analytics.

The interpreter to use for the import of each line is specified by the `{interpreter-name}` parameter. This name is the name given to the interpreter that is mentioned in the
annotation within the stored procedure.

The interpreter with the given name should be present in the datastore, and must already be loaded for the interpreter to apply. Redeploying the interpreter code will result in the new interpreter being used as soon as the new one is loaded.

If the interpreter being used is removed and underplayed from the datastore, it will result in cancellation of the watch service. You will have to restart the watch service with a new interpreter or no interpreter at all.

The same interpreter class can be used with multiple watch services.

More information on writing interpreters can be found in the stored procedures section.
{% include links.html %}
