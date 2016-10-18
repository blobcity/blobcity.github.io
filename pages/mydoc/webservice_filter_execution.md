---
title: Filter Execution
sidebar: mydoc_sidebar
permalink: webservice-filter-execution.html
folder: mydoc
---

## Filter Execution

The filter allows for high speed scan thought all records in a specific collection. The collection name on which the filter is to be executed needs to be specified in the request. A filter can only scan one table on one invocation, but the same filter may be used for multiple tables.

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "c" : "collection1",
  "q" : "filter",
  "p" : {
    "name" : "HelloWorld",
    "p" : {
      "param1" : "value1"
    }
  } 
}
```
The name of the filter to execute is provided as the name parameter. The secondary payload is used to initialise any parameters for the filter, such as the search condition to filter on. This is an optional parameter and can be ignored for filter that do not require any initialisation parameters.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : []
}
```
The response comprises of a JSON array. Each element of the array is the response given by the filter against a single record that was checked against the filters. The records that give a null response to the filter operation, are ignored. The elements of the JSON array are completely user defined and are exactly provided in the manner as returned by the filter execution. No guarantees of any sort are given on the order of elements in the JSON array.
{% include links.html %}
