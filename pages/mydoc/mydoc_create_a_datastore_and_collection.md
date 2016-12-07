---
title: Create a Datastore and Collection
sidebar: mydoc_sidebar
permalink: create-a-datastore-and-collection.html
folder: mydoc
---

## Create a Datastore and Collection

An empty datastore and collection can be created from the CLI. The datastore needs to be created first as the collection will then be created inside a datastore. The database by default comes with a datastore called `.systemdb`. This means you cannot create another datastore with the same name. Also even the `root` user does not have permission to modify the schema of that datastore, so it’s structure cannot be changed.

The following command fired over the CLI creates a new datastore with name `ds1`

```
blobcity>create-ds ds1
Datastore successfully created
```

A confirmation message is displayed if the command is successful in creating the datastore. Now that the datastore is created, a collection can be created within the datastore. The following command creates an `on-disk` collection within `ds1`.

```
blobcity>create-collection ds1.collection1 on-disk
Collection successfully created
```

A confirmation message is displayed if the command is successful in create the collection. collection1 is the name of the collection. The on-disk parameter indicates that any data to be added to the collection will be stored on on the file system.

BlobCity has two storage engines, one for file system storage and the other for memory storage. Specifying the collection to be `on-disk` indicates that the collection should use the file system based storage engine. Other types of storage options that can be specified are `in-memory` and `in-memory-non-durable`. Both the memory storage types store all data in memory. The in-memory type storage is a persistent storage, where all data needs to reside on memory, but is serialised to disk so that the data is not lost if the server reboots. The in-memory-non-durable is intentional non-persistent storage, where the data is all stored in memory and never persisted to disk with the expectation that it will be lost when the server is rebooted.

The non-durable storage is used for storing non critical data, or data that has a master copy stored somewhere else. The non-durable nature is chosen to make the memory store very fast, whereby in BlobCity a non-durable collection is expected to take 10 times as many transactions per second as compared to a durable collection.

{% include links.html %}
