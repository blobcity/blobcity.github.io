---
title: Saving or updating a record
sidebar: mydoc_sidebar
permalink: webservice-delete-data.html
folder: mydoc
---

## Saving or updating a record

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "save",
  "p" : {
    "_id" : "record-id",
    "data" : {
      "col1" : "value1"
    }
  } 
}
```

A record if found with the specific `_id` within the specified collection is replaced with the provided data object. The `_id` is required for identification of the record to be modified. The `_id` can be provided optionally as a column within the record instead of explicit inclusion as an `_id` key in the payload.

If the `_id` key is included in the payload, and an `_id` field is present in the data record, the operation will delete the record with the explicitly specified `_id` and create a new record with the `_id` value as mentioned in the actual record. This process can be used to update user defined `_id` values of records. The operation will succeed so long as there is no second record with the same `_id` as the `_id` mentioned in the record object.

The provide `data` object can be of any format. The new data record provided does not have to be same format as the existing record. SQL data in the form of `INSERT INTO` query is not supported for an update operation.

The save operation by default updates if a record with the specified `_id` is present, or else inserts. So if this operation is executed with an invalid `_id`, the operation will succeed by inserting a new record into the collection. This is the default behaviour and is not customisable to restrict inserts.

**Incremental Updates**
s
"p" : {
    "_id" : "record-id",
    "data" : {
      "col1" : "value1"
    }
    "overwrite" : false
{% include links.html %}
