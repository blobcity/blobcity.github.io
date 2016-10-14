---
title: Commands 
sidebar: mydoc_sidebar
permalink: cli-authentication.html
folder: mydoc
---

## Command Format

All CLI requests start with a command code. The command code instructs the database of the operation the user wishes to perform as part of that request. Each support operation has a unique command code. An example command is shown below.
```
blobcity>create-ds datastore1
```

In the above command `create-ds` is the command code and `datastore1` is the command parameter. All commands need to always start with a valid command code. `datastore1` is a parameter supplied to the create-ds command, and the parameter formats varying from command to command. This particular command creates a new datastore with the specified name of datastore1.

The `blobcity>` shown at the beginning of the command is actually not typed by the user. This is displayed by default by the CLI interface, to indicate to the user that the user is
successfully logged into the CLI and the CLI is ready to accept a new command.

## SQL Execution

This request allows for execution of any SQL on the database. The SQL can be for data select, data insert, schema modification or any other SQL query based operation supported by BlobCity. The SQL query needs to be executed within the mentioned data store and the query structure needs to match the query grammar supported by BlobCity to prevent an error.

The response for the SQL query depends on the query. This query has significant variations in the payload response. Responses to some of the most commonly used SQL query types are mentioned further in this section.

**Select Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "data" : [{"json" : "data"},"XML","CSV","Text"]
  }
}
```
Any SQL query intended for fetching data, responds back with the matched records containing the matched columns. The response is heterogeneous and cannot be forced to be type converted to a specific format. The ordering of CSV results is the order of insert for `SELECT *` queries. If specific columns are specified, the order of the column values in the CSV record match the order in which the columns were requested in the query.

**Insert Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "id" : "id-of-new-record"
  }
}
```

The `INSERT INTO` SQL query responds with the primary key of the record that is inserted. The primary key is the value of the `_id` column, either auto-generated or explicitly specified in the insert. If the insert operation fails for any reason, including rejection of the insert due to duplicate primary key, or any other rule / condition violation; the response will be a failed response with `ack` value of `0`. In case of the failed response, the error code will allow for identification of the reason for failure.

**Update / Delete Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    “rows-affected" : 1
  }
}
```

SQL querying performing an update or delete operation, provides the count of the number of rows affected by the operation as a response. A `rows-affected` value of `0` indicates the operation was successfully executed, but nothing was changed as the update or delete condition was never satisfied. An error in execution will be responded with a `ack 0`.

## Create Datastore

This simple request creates a datastore if another datastore with the same name is not already present. The ds parameter is used as the name of the datastore that will be created.

```
{
  "username" : "root",
  "password" : "root",
  "q" : "create-ds",
  "p" : {
    "name" : "datastore1"
  }
}
```

The user must have the necessary permission to create a datastore for this operation to succeed. If you are using BlobCity on a multi-tenant cloud environment, then this option will not be available to you. You will have to use the BlobCity database management portal to create the datastore.

**Response Structure**

```
{
"ack" : "1",
  "time" : 1000
}
```

The response acknowledges creation of the datastore. If creation fails an `ack` value of `0` is returned along with the cause that allows further diagnosis of the error.

## Create Collection

Creates a new collection within the specified data store. The collection name is specified by the `name` parameter in the payload. The `type` parameter in the payload allows for specifying the storage type for the collection. The storage type can be one off `in-memory`, `on-disk` and `in-memory-non-durable` or `in-memory-nd`. The type parameter is optional and if none is specified it defaults to `in-memory`.

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory"
  }
}
```

**Specifying a replication type**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory",
    "replication-type" : "distributed",
    "replication-factor" : 2
  } 
}
```

When no `replication-type` is specified the table is created with a default `replication-type` of distributed, with `replication-factor` set to `2`. This means the data in the collection will be shared when the database is running as a cluster, and 2 copies of each data point will be stored across nodes in the cluster. The above request does exactly same as the request without the `replication-type` specified, but can be used if another replication strategy is to be supported, or a different `replication-factor` is required.

The supported replication factors are distributed and mirrored. The distributed replication factor does data sharding, while maintaining the specified number of backup copies of each data record. The mirrored replication strategy on the other hand, makes sure that all data points are present on all nodes in the cluster. The mirrored strategy is good for small tables, master tables and the smaller of two tables that are part of a distributed join query.

**Creating a mirrored type collection**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "create-collection",
  "p" : {
    "name" : "collection-name",
    "type" : "in-memory",
    "replication-type" : "mirrored"
  } 
}
```

The query request creates a table with `replication-type` of `mirrored`. Note that there is no `replication-factor` parameter for a `mirrored` type collection, as all data in the collection is always replicated across all nodes in the cluster. The replication is consistent with new nodes that are added to a cluster on a mirrored collection with existing data.

**Response Structure**

```
{
"ack" : "1",
  "time" : 1000
}
```

Provides a simple acknowledgement indicating whether the collection was created or not.

{% include links.html %}
