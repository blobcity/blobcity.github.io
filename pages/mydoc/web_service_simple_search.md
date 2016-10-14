---
title: Simple Search
sidebar: mydoc_sidebar
permalink: simple_search.html
folder: mydoc
---

## Using BlobCity over RESTful web services

Whether On-Cloud or On-Premise, the BlobCity Database can be fully used over a RESTful web service interface. Some of the language specific adapters themselves, communicate with the database over these REST interfaces. The REST support is very exhaustive and extends to every action that can be taken on the database.

## Cloud Connection Endpoint
To connect to any cloud instance of BlobCity, the REST connection URL mentioned is

```
http://{data-centre-id}.db.blobcity.com/rest/bquery
```

The `{data-centre-id}` is the id of the data centre on which you are running your BlobCity instance. The id usually comprises of the major data centre provider code
followed by the region code of the data centre. For connecting to AWS instance on US East (N. Virginia) the code would be aws-us-east-1 and the endpoint would be `http://aws-
us-east-1.db.blobcity.com/rest/bquery`

The complete list of upto date data centre codes can be found from the API details section on your cloud portal account. They are also mentioned in [Appendix 3] for quick reference, but you should note that the list is ever changing, and the Appendix 3 may be outdated, by the time you are reading this.

## On-Premise Connection Endpoint
The BlobCity RESTful end point on your location installation by default can be accessed as

`http://localhost:10111/rest/bquery`

`http://{ip}:{port}/rest/bquery`

The default port is 10111 for the endpoint, but is changeable to a port of your choice.

The operation request is sent to this end point in the form of a JSON object for a POST call. The rest of the chapter focuses on the request and response formats for the various supported operations.

## Generic Request Format
Each request end point takes a JSON request data as a POST request. The JSON has a generic format across all query types and operations. At a high level the JSON formats are split into data format and management format. The data format is used for queries that operate on data such as data reading and data modification. The management format is suitable for managing the database, including schema management and system level management of users, nodes, backup amongst other items.

**Generic Management Query JSON Request**

```
{
  "username" : "root",
  "password" : "root",
  "q" : "{query-type}",
  "p" : {
  } 
}
```

The username and password of the user that will access the system needs to be always provided. The q parameter specifies the query code for the query. The p is a payload specifying the payload corresponding to the query code provided. If the payload does not abide by the format specifications required for the specific query code, an error will be thrown.

For all management queries, the only thing that will change per query is the payload that is sent for the corresponding query type. The payload is a JSON object within the primary JSON object, and should be readable by the database as a sub JSON to prevent an error.

**Generic Data Query JSON Request**

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "data-store-name",
  "c" : "collection-name"
  "q" : "{query-type}",
  "p" : {
  } 
}
```

The additional mandatory parameters for any data related operations include the name of the data store and name of the collection on which the operation is to be performed. If the query type is not a data query, the ds and c parameters will be ignored from request processing. The payload in these types of requests, typically will contain data or collection schema.

In some exception data queries that span across tables, the collection name attribute may be skipped. A join query that spans multiple takes needs to be executed as a SQL query for which the collection name should not be specified as the query is not limited to a single collection. The data store name however needs to be provided for all data queries.

It is important to remember here, that no query can span across collections in two separate data stores. All queries, no matter how many collections they span, will have to operate under a single specified datastore.

## Generic Response Format

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
  }
}
```

The response format contains an acknowledgement stating whether the response is a success response or an error response. An ack value of 1 indicates a success response, while an ack value of 0 indicates an error response.

The response always contains the time in milli seconds that the request took to process on the database. These values are measured between request registration and response generation at the database level. Network latencies are not counted in this time, so it is a good enough rough measure of the performance delivered by the BlobCity cluster for the specific request. This value is not a benchmark, but provided for simple study purpose.

Each success response has only an associated payload that contains information relevant to the response. The payload can be either a JSON object or a JSON array depending on the type of the query against which this response is produced.

**An error response**

```
{
  "ack" : "0",
  "code" : "error-code",
  "message" : "error description message",
}
```

The error response have an ack value of 0 and in addition specifics the error code and a message that describes the error in a humanly readable manner. The message may contain additional information that allows better diagnosis of the problem. The complete list of error codes are listed in Appendix 2

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
