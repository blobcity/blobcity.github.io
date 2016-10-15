---
title: Configuring BlobCity
sidebar: mydoc_sidebar
permalink: configuring.html
folder: mydoc
---

## Accessing Database over CLI

The Command Line Interface (CLI) is the easiest and most developer friendly mechanism to perform operations on BlobCity DB. The CLI is permitted over the network and hence is actually a TCP stream. This means you do not have to be on the local terminal of the machine on which the database is running to use the CLI of the database.

The default connection to CLI is over port 10113. From a linux terminal the following command will get you connected to the CLI.

```shell
telnet localhost 10113
```
OR

```shell
telnet <ip> 10113
```
The `<ip>` allows for connecting to a remote database instance. You will be required to enter a valid username and password that you wish to use to connect to the database. On connection a greeting message will be displayed, and the console will be ready to accept further commands. Sample console shown below.

```
telnet localhost 10113
Trying ::1...
Connected to localhost.
Escape character is '^]'.
username>root
password>root
You are now inside the BlobCity DB console
Type 'help' for assistance and 'exit' to quit
blobcity>
```
All on-premise / dedicated instance of BlobCity ship with a default user named `root`. The password of the `root` user is also `root`. The root user has full administrative rights on the database. It is highly recommended that you change the password of the `root` user, or create new users and delete the `root` user as soon as your instance is setup.

## Create a Datastore and Collection

An empty datastore and collection can be created from the CLI. The datastore needs to be created first as the collection will then be created inside a datastore. The database by default comes with a datastore called `.systemdb`. This means you cannot create another datastore with the same name. Also even the `root` user does not have permission to modify the schema of that datastore, so it’s structure cannot be changed.

The following command fired over the CLI creates a new datastore with name `ds1` 

```shell
blobcity>create-ds ds1
Datastore successfully created
```

A confirmation message is displayed if the command is successful in creating the datastore. Now that the datastore is created, a collection can be created within the datastore. The following command creates an `on-disk` collection within `ds1`.

```shell
blobcity>create-collection ds1.collection1 on-disk
Collection successfully created
```

A confirmation message is displayed if the command is successful in create the collection. collection1 is the name of the collection. The on-disk parameter indicates that any data to be added to the collection will be stored on on the file system.

BlobCity has two storage engines, one for file system storage and the other for memory storage. Specifying the collection to be `on-disk` indicates that the collection should use the file system based storage engine. Other types of storage options that can be specified are `in-memory` and `in-memory-non-durable`. Both the memory storage types store all data in memory. The in-memory type storage is a persistent storage, where all data needs to reside on memory, but is serialised to disk so that the data is not lost if the server reboots. The in-memory-non-durable is intentional non-persistent storage, where the data is all stored in memory and never persisted to disk with the expectation that it will be lost when the server is rebooted.

The non-durable storage is used for storing non critical data, or data that has a master copy stored somewhere else. The non-durable nature is chosen to make the memory store very fast, whereby in BlobCity a non-durable collection is expected to take 10 times as many transactions per second as compared to a durable collection.


{% include links.html %}
