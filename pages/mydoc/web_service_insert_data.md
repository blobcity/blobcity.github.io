---
title: Insert Data
sidebar: mydoc_sidebar
permalink: insert-data.html
folder: mydoc
---

## Inserting Data

```json
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "insert",
  "p" : {
    "data" : ["XML","JSON",{"key":"json"},"Text"]
  } 
}
```

The data being inserted can be of any of the supported formats by BlobCity. The database does an automatic format interpretation for JSON, XML and SQL data types. All other data types are stored as plain text in string.

The `data` key is mapped to a JSON array of String. This allows for multiple records to be inserted in a single call. The records in the JSON array can be heterogeneous formats. JSON data can be put as a JSON object into the JSON array, instead of a being putting as a JSON String into the array. Both JSON record as is and a string form of the JSON record is supported. All other records must be passed as their string equivalents.

**Explicitly specifying data format**

```
"p" : {
    "type" : "csv",
    "data" : ["val1,val2","val3,val4"]
  }
```

The format of data can be explicitly specified by adding the `type` parameter within the payload. This forces all data within the array to be of the specified type. Records that are not of the specified type will be skipped from the insert operation, while other records which are of the correct format will be inserted.

The supposed data formats as part of the type parameter are `json`, `xml`, `sql`, `csv`, `text`, `auto`. The `auto` type allows for heterogeneous data types within the array and requests for an automatic type detection of the data. The type parameter is checked in a case insensitive manner, and not specifying a type parameter default behaviour to same as specifying a type parameter of auto.

For `sql` type data only `INSERT INTO` SQL commands are interpreted. The data specified must be a SQL query string corresponding to a valid `INSERT INTO` SQL command.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "status" : [1,0,1,1],
    "ids" : ["id1","","id3","id4"],
    "inserted" : 3,
    "failed" : 1
  } 
}
```
The response throws out the `status` for each item that was attempted to be inserted. The status is an array of `1` and `0` numbers, where the number  `1` indicates that the corresponding record was successfully inserted, while the number `0` indicates a failed insert. The status array is guaranteed to comprise of the same number of elements as the insert request with the response status being in the same order as the order of the records in the request.

The `ids` of all records are also returned back. BlobCity by default produces an auto generated record id, unless one is specified as a `_id` field in the data being inserted. Assuming the record does not specify any `_id`, a blank value is returned for each failed record, while the internally auto generated `_id` is provided for all successfully inserted records. For a record that explicitly specifies an `_id`, but fails in inserted due to some user configured condition or formula restriction, the specified `_id` will be provided in the response along with the status of `0` for the corresponding record. A sample payload for one failed record with a manually specified `_id` in the request is shown below.

```json
"p" : {
    "status" : [1,0,1,1],
    "ids" : ["id1","id2","id3","id4"],
    ...
}
```

{% include links.html %}
