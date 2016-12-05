---
title: Saving or updating a record
sidebar: mydoc_sidebar
permalink: webservice-update-record.html
folder: mydoc
---

## Update Operation

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "update",
  "p" : {
    "set" : {
      "col1" : "value1"
    },
    "where" : [
      {"c" : "_id", "x" : "EQ", "v" : "val"}
    ]
  } 
}
```

The operation updates all records that matches the `where` condition. The operation allows setting of specific values to specific columns, for all records that match the criteria. Irrespective of the format of the actual record, the column values that have to be set have to be passed as a JSON object. The structure of the JSON objects comprises of the key as the name of the column and the value corresponding to the key is the value which is to be set to the column. The `set` parameter is passed for setting the values. Multiple column values can be set in a single operation, by passing as many column value pairs as required in the `set` parameter JSON.

**Updating with multiple conditions**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "update",
  "p" : {
    "set" : {
      "youth" : true,
      "allow-driving" : false
    }
    "where" : [
      {"c" : "gender", "x" : "EQ", "v" : "M"},
      {"c" : "age", "x" : "LT", "v" : 15}
    ],
    "association" : "AND"
  }
}
```

The above request updates values of multiple columns in a single request for all records that satisfy the multiple search conditions put. The `association` parameter is optional and defaulted to `AND` if none specified.

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

The response simply provides the number of rows that were updated by the operation. A value of `0` indicates a successful operation execution, with no records found matching the search condition for performing an update.

{% include links.html %}
