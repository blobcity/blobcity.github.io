---
title: JSON Storage
sidebar: mydoc_sidebar
permalink: multi-model-storage-json.html
folder: mydoc
---

## JSON Storage

Fully interprets JSON data. Each record needs to be a valid JSON object. The object may internally contain any level of JSON nesting and may contain JSON arrays. The keys of all elements must be of a String type while the values can be of any type. The system will automatically perform a type inference.

A schema inference engine, infers the schema of the JSON object. The inferred data is then operable using any of the BlobCity supported queries. The JSON data can only be loaded into a collection, with each JSON object comprising of one record in the collection.

When a JSON is imported, the keys get mapped to the column name. If a column with the same name is already presented in the collection, the value of that key is added as a value into that column. A new column with the key name is created if one is not already provided. Any level of JSON nesting is permitted, with nested JSON columns being named by concatenating names of nested keys separated by a ‘.’ (dot) separator between the key names.

Let us consider starting with an empty table and then inserted our first JSON record into it. 

Consider the insert of the below mentioned JSON record

```json
{
  "name" : "John",
  "age" : 45 
}
```
The collection after insert of the single JSON record looks as mentioned below.

**Collection with 1st JSON record inserted

_id | name | age
----|----|----|
xxx | John | 45

It is interesting to note that two new columns got added into the table on successful insert of the JSON. Additional inserting the below JSON will added a record to the table.

```
{
  "name" : "Tom",
  "age" : 26 
}
```

**Collection with a2nd JSON record inserted

_id | name | age
----|----|----|
xxx | John | 45
xxx | Tom | 26

Each record is automatically provided an `_id` value is that acts as primary key. This value is unique within the collection. However if a user wants to provide an explicitly defined primary key, the same can be done by inserted a JSON record with a specified `_id` field. The new record will get inserted with the specified `_id` field as long as another record with the same `_id` value is not already present. The `xxx` in the above table representations is a simple placeholder notation for an auto-defined value.

An insert of a JSON object with an explicitly specified `_id` value and the corresponding entry added into the table is shown below.

**Collection with 3rd JSON record having an explicitly specified _id value

```
{
  "_id" : "1000",
  "name" : "Mary",
  "age" : 30
}
```

{% include links.html %}
