---
title: Exit
sidebar: mydoc_sidebar
permalink: cli-exit.html
folder: mydoc
---

## Simple Search

The search query allows firing a single table simple search over columns of the table. This query runs on all formats of multi-model storage supported, as long as the column names abide by the schema inferred by BlobCity.

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "search",
  "p" : {
    "from" : ["collection-name"],
    "select" : ["*"],
    "where" : [
      {"c" : "col1", "x" : "EQ", "v" : "val"},
      {"c" : "col2", "x" : "LT", "v" : 10},
      {"c" : "col3", "x" : "IN", "v" : [10,12]}
],
    "association": "AND"
  }
}
```

The search query allows firing a single table simple search over columns of the table. This query runs on all formats of multi-model storage supported, as long as the column names abide by the schema inferred by BlobCity.

The parameters of the search query are specified within the payload. The `from` parameter contains the list of collections that comprise of the search query. As of this point only a single collection name per request is supported. The collection name is acquired in the form of a JSON array of strings. In future querying data across multiple collections will be provided.

The `select` parameter specifies the columns that are sought as response. A value of * indicates that all columns in the collection are to be selected. For selecting specific columns only, the list of column names to select can be provided. Columns specified here are the columns that are sought in the result set and have nothing to do with the columns involved in the search condition.

The `where` parameter defines the search condition. The search criterial is provided as an array of JSON objects. Each JSON object within the where clause maps to a condition on a single column. In the condition c indicates the name of column, v indicates the search value and x indicates the search operation. The list of supported search operations along with the specified operation code to be used as the x parameter is mentioned in the table below.

The `association` parameter is optional and required when only more than one search condition is provided. It provides the linkage between the various search conditions. A value of `AND` means all conditions have to be satisfied for a record, for the record to be included in the search results. A value of `OR` means if either of the conditions is satisfied for a record, the record will be included in the search results. Only `AND` and `OR` are the two associations allowed at this point. If no association parameter is mentioned and multiple where conditions are passed, it will default to an `AND` operation.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "data" : [{"json" : "data"},"XML","CSV","Text"]
  }
}
```

The response contains the payload as a JSON array with the `data` key, containing all the records that match the search condition. The search results can be of heterogeneous format depending on the data inserted into the collection. An empty JSON array is returned if no records match the search condition.

If only specific columns are requested, the default records will be modified to remove the unwanted values and then returned in the respective format of the data. For CSV data, the response will be in the same sequence as the insert if a select * is performed. When selecting only specific columns for a CSV data, the response will be in CSV format containing only the requested columns, in the exact order in which they were requested.

**Requesting in a specific data format**

If you wish to get the response in a homogeneous format on a table that contains heterogeneous data points, or wish to retrieve data in a format different from the format in which the data was inserted, the same can be done using an additional as parameter in the request payload. An example payload that forces all non JSON data to be converted to JSON and returned is mentioned below.

```
"p" : {
    "from" : ["collection-name"],
    "select" : ["*"],
    "where" : [
      {"c" : "col1", "x" : "EQ", "v" : "val"},
    ],
    "as" : "json"
  }
```

The supported formats in the `as` clause are `json`, `xml`, `csv`, `text` and `sql`. In case of choosing sql, the data will be returned as `INSERT INTO` SQL queries corresponding to each record. When requesting data in `csv` format, the column names are mentioned as an additional parameter in the response. This is the case only if the requested columns are *. If requesting specific columns only, then the response columns will be in the order of the request as part of the `select` criteria.

A sample response for `select *` with format `as csv` is mentioned below. The additional `cols` parameter provides the reading order for each of the CSV records in the result.
```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "data" : ["val1,val2,val3", "val4,val5,val6"],
    "cols" : ["col1", "col2", "col3"]
  }
}
```

{% include links.html %}
