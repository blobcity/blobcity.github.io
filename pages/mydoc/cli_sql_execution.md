---
title: SQL Execution
sidebar: mydoc_sidebar
permalink: cli-sql-execution.html
folder: mydoc
---

## SQL Execution

```
blobcity>sql {ds}: {sql-query}
```

This request allows for execution of any SQL on the database. The SQL can be for data select, data insert, schema modification or any other SQL query based operation supported by BlobCity. The SQL query needs to be executed within the mentioned data store and the query structure needs to match the query grammar supported by BlobCity to prevent an error.

The `{ds}` parameter specifies the datastore inside which the SQL is to be executed. The the specified datastore should be present, and the logged in user should have access to the datastore and permission to run the specific query for the operation to succeed.

Depending on the query, the response will be shown in the simplest possibly human readable form. Any data returned by queries such as select queries are expected to be in JSON result set format, similar to the response giving by the corresponding REST web service counterpart.
{% include links.html %}
