---
title: Delete Data
sidebar: mydoc_sidebar
permalink: webservice-delete-data.html
folder: mydoc
---

## Delete Data

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "delete",
  "p" : {
    "where" : [
       {"c" : "_id", "x" : "EQ", "v" : "val"}
    ],
  } 
}
```
The above request deletes a record by its primary key. This is the simplest form of deleting a specific record from the database. The where condition is similar to the where for a search query. Complex delete operation that match a specific condition can also be executed to bulk delete data.

**Deleting over a complex condition**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "delete",
  "p" : {
    "where" : [
      {"c" : "gender", "x" : "EQ", "v" : "M"},
      {"c" : "age", "x" : "LT", "v" : 21}
    ],
    "association" : "AND"
  }
}
```

An exhaustive where clause can be put in to delete all records that satisfy the where condition. The `association` parameter is optional and can take a value of `AND / OR`, and is used to specify the correlation between multiple where conditions. The association is ignored for a single condition where clause, and is defaulted to `AND` if no association is specified for multiple where conditions.

**Deleting all records**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "delete",
  "p" : {
    "where" : [
      {"c" : "_id", "x" : "NEQ", "v" : ""}
    ]
  } 
}
```

The above request will result in truncating the entire collection without warning. This is the same because the `_id` column is a mandatory non null and non empty column. Deleting all items where `_id` is not empty essentially defaults to all records in the collection, thus resulting in the entire collection to be truncated.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "rows-affected" : 1
  }
}
```
The response simply provides the count of the number of records that are deleted as part of the delete operation. If the delete operation does not affect any records the `rows-affected` count will be `0`. An `affected-rows` value of `0` indicates a successful delete operation. An `ack` value of `0` can be used to identify failure of the delete operation, along with cause of failure.

{% include links.html %}
