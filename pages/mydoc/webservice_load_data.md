---
title: Load Data
sidebar: mydoc_sidebar
permalink: webservice-load-data.html
folder: mydoc
---

## Load Data

The load command allows loading of data by their primary keys. This is the fastest and simplest way of picking up specific records from the database. This function may rarely be used by some apps that allow BlobCity to auto-generate all primary keys, but is still provided for sake of convenience.

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "load",
  "p" : {
    "ids" : ["id1","id2","id3"]
  }
}
```
All records corresponding to the specified `ids` are selected from the database. Id’s that are in-existent or cannot be found in the collection are simply ignored and nothing is returned
for those id’s.

**Response Structure**
```
{
  "ack" : "1",
  "time" : 1000,
  "p" : ["XML record", {"json": "record"}, "CSV record", "Text record"]
}
```

The records as returned as a payload of JSON array. All types of records, other than JSON records are returned in the form string elements. Records that were inserted natively as JSON are returns as JSON object elements. Records that were inserted as SQL insert queries, are returned as JSON objects.

{% include links.html %}