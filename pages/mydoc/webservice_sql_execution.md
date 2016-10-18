---
title: SQL Execution
sidebar: mydoc_sidebar
permalink: webservice-sql-execution.html
folder: mydoc
---

## SQL Execution

This request allows for execution of any SQL on the database. The SQL can be for data select, data insert, schema modification or any other SQL query based operation supported by BlobCity. The SQL query needs to be executed within the mentioned data store and the query structure needs to match the query grammar supported by BlobCity to prevent an error.

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "sql",
  "p" : {
    "sql" : "select * from `datastore1.collection1”
  }
}
```

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

SQL querying performing an update or delete operation, provides the count of the number of rows affected by the operation as a response. A `rows-affected` value of `0` indicates the
operation was successfully executed, but nothing was changed as the update or delete condition was never satisfied. An error in execution will be responded with a `ack 0`.
{% include links.html %}
