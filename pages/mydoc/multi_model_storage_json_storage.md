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

An empty table looks as represented below:

**Empty table with a single _id (primary key) column**

| _id |
|-----|
|     |

Consider the insert of the below mentioned JSON record

```json
{
  "name" : "John",
  "age" : 45 
}
```
The collection after insert of the single JSON record looks as mentioned below.

**Collection with 1st JSON record inserted**

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

**Collection with 2nd JSON record inserted**

_id | name | age
----|----|----|
xxx | John | 45
xxx | Tom | 26

Each record is automatically provided an `_id` value is that acts as primary key. This value is unique within the collection. However if a user wants to provide an explicitly defined primary key, the same can be done by inserted a JSON record with a specified `_id` field. The new record will get inserted with the specified `_id` field as long as another record with the same `_id` value is not already present. The `xxx` in the above table representations is a simple placeholder notation for an auto-defined value.

An insert of a JSON object with an explicitly specified `_id` value and the corresponding entry added into the table is shown below.

**Collection with 3rd JSON record having an explicitly specified _id value**

```
{
  "_id" : "1000",
  "name" : "Mary",
  "age" : 30
}
```

## Nested JSON’s

```
{
  "name" : "Stacy",
  "age" : 43,
  "addr" : {
    "line1" : "line1",
    "line2" : "",
    "state" : "IL",
    "zip" : "60002"
  } 
}
```

The above JSON contains a nested JSON mapped to the key `addr`(address) .The above JSON when inserted on our table, creates additional fields for each of the sub-elements present within the `addr` JSON. The additional column are automatically produced. The new table looks as below.

**Table post insertion of a nested JSON**

| _id | name | age | addr.line1 | addr.line2 | addr.state | addr.zip | 
|-----|------|-----|------------|------------|------------|----------|
| xxx | John | 45 | 
|xxx | Tom | 26 |
|1000 | Mary | 30 |
| xxx | Stacy | 43 | line1 | IL | 60002 |

It is important to note that none of the new records were actually affected by this operation. Although it looks like the records for John, Tom and Mary got 4 new columns, that is not the case when you fetch those records. The original records are in no way affected by insertion of the new records.

The insert however results in new columns getting created. The columns are named as the element key followed by the sub-key separated by a dot in between as in `addr.line1` indicating that line1 is an element present within the `addr` JSON object. Such naming conventions can cause problems if you have another root level element named `addr.line1`. The database cannot differentiate between the two, and it will result in the same column getting two values that are searchable as if there was JSONArray object associated with the `addr.line1` key. We will discuss this further when we cover how JSONArrays are handled.

The created columns will remain part of the schema unless explicitly deleted, even if the record for Stacy is deleted. Explicitly deleting a single column will result in the JSON record being modified to as if the JSON record had everything other than the column that was deleted.

## Selecting records

```
SELECT * FROM db1.users
```

The query selects all records from the `users` collection. Let us assume that the above mentioned table was called `users` and was placed inside a datastore called `ds1`. The response will be received as a JSONArray, with each element of the array comprising of an individual JSONObject. The response to the above query on our users tables is as shown below:

```
[
  {"name": "John", "age": 45},
  {"name": "Tom", "age": 26},
  {"name": "Mary", "age": 30},
  {"name": "Stacy", "age": 43, "addr": {
    "line1": "line1",
    "line2": "",
    "state": "IL",
    "zip": "60002"
    }
  } 
]
```

It should be noted that the records for John, Tom and Mary did not include any entry for the `addr` field that is present only for the record of Stacy. It is also important to note that the response did not contain the `_id` field that is allotted to the each record. The `_id` is skipped by default in responses as it is meant to be an auto-defined field for internal use only. If you wish to fetch the value of the `_id` field, the same can be explicitly specified in the select query.

**Selecting the _id field**

```
SELECT *,_id FROM db1.users
```

The above query requests for the `_id` value to be selected as part of the SQL query along with selecting all other columns present in the `users` collection. The response for this case is as shown below:

```
[
  {"_id": "xxx", "name": "John", "age": 45},
  {"_id": "xxx", "name": "Tom", "age": 26},
  {"_id": "1000", "name": "Mary", "age": 30},
  {"_id": "xxx", "name": "Stacy", "age": 43, "addr": {
    "line1": "line1",
    "line2": "",
    "state": "IL",
    "zip": "60002"
    }
   } 
]
```

Again over here the `xxx` value for `_id` is just a placeholder representation for an auto- defined value. The response will contain the auto-defined value that the database allotted to each of the records in place of the `xxx`.

**Selecting specific columns**

If the whole record is not required, only specific columns can be selected. The response is an array of JSONObject’s with each JSONObject containing only the selected column. The SQL query for selecting only the name columned and the corresponding JSON response is mentioned below.

```
SELECT name FROM db1.users

[
  {"name": "John"},
  {"name": "Tom"},
  {"name": "Mary"},
  {"name": "Stacy"}
]
```

Selecting a nested column will only contain records that have the nested column present. The other records will not be returned as part of the select response.

```
SELECT addr.zip FROM db1.users

[
  {"addr": {
    "zip" : "60002"
  }}
]
```

**Selecting a nested JSON**

In case we want only the address information for all records, the same can be searched by mentioning the key of the nested JSON object in the query query. In the case of our users collection, selecting by a column named `addr` will pickup all records present inside the `addr` entry. It is important to note that in our actual schema there is not actual column called `addr`. So you cannot fire a search query on `addr`, but you can specify `addr` as a column name in a select query to represent the complete nested JSON object mapped to the `addr` field inside the primary record.

```
SELECT addr FROM db1.users

[
  {"addr": {
    "line1": "line1",
    "line2": "",
    "state": "IL",
    "zip": "60002"
  }} 
]
```

## Handling JSON Arrays
A JSON object can internally contain an array. This array can be an array of primitive elements, or an array of JSON objects itself. The arrays in JSON are heterogeneous and not all elements have to be on the same type. BlobCity supports storage, search and retrieval of any types of JSON arrays present within JSON objects. Storage of JSON array without it being a part of a JSON object is however not yet supported.

Let us consider our original users table having just two columns of `name` and `age` over and above the auto-defined column of `_id`. For the same of simplicity we will drop the `addr` nested JSON and associated columns in this section.

```
{
  "name" : "John"
  "age" : 45,
  "likes": ["music", "swimming"]
}
```

If the above JSON is inserted into a new table, the following structure is created.

| _id | name | age | likes |
|-----|------|-----|-------|
| xxx | John | 45 | [“music”, “swimming”] |

The likes columns is created as a collections type, that allows for the multiple values to be present in a single cell. Search can be performed on the likes column, where each item of the array can be looked up as if it was an item belonging to individual records. Let’s first look at a select query that is fired on this table and the expected response from the select query.

```
SELECT * FROM ds1.users

[
  {
  "name" : "John"
  "age" : 45,
  "likes": ["music", "swimming"]
  }
]
```

The select returns the array in its original form. The order of the elements within the array is however not guaranteed so the response could also be as shown below.

```
[
  {
  "name" : "John"
  "age" : 45,
  "likes": ["swimming", "music"]
  }
]
```

Notice the reverse in order of the values `swimming` and `music` inside the `likes` array. Both are valid response for the query against the record that was inserted.

A search can also be performed on the array elements as demonstrated by the following SQL query and corresponding response.

```
SELECT * FROM ds1.users WHERE likes = 'music'
[
  {
  "name" : "John",
  "age" : 45,
  "likes": ["swimming", "music"]
  }
]
```

The response essentially checks for a presence of the element `music` inside the `likes` column. Multiple conditions checks can also be performed on the array elements. For studying how more SQL queries response, let us consider the below table.
| _id | name | age | likes |
|-----|------|-----|-------|
| xxx | John | 45 | [“music”, “swimming”]
| xxx | Tom | 26 | [“music”, “football”]
| 1000 | Mary | 30 | [“tennis”]

Let us reattempt the same SQL with a where clause to search for all users that like music.

```
SELECT * FROM ds1.users WHERE likes = 'music'
[
  {
    "name" : "John",
    "age" : 45,
    "likes": ["swimming", "music"]
  }, 
  {
    "name" : "Tom",
    "age" : 26,
    "likes": ["music", "football"]
  } 
]
```
It can be observed that all users that have music listed in their likes are selected. The record for Mary is not selected and her likes to do not include music. Let us see what happens if we are looking for all users that have music and swimming as likes.

```
SELECT * FROM ds1.users WHERE likes = 'music' AND likes = 'swimming'
[
  {
    "name" : "John",
    "age" : 45,
    "likes": ["swimming", "music"]
  } 
]
```

Such a query would not make sense on traditional SQL tables, as one would always expected an empty result set. This is so because the same column cannot be equal to two values at the same time. However such a query works beautifully within the BlobCity DB to check for `AND` associations between different elements in an array type column.

```
SELECT * FROM ds1.users WHERE likes = 'music' OR likes = 'tennis'

[
  {
    "name" : "John",
    "age" : 45,
    "likes": ["swimming", "music"]
  }, 
  {
    "name" : "Tom",
    "age" : 26,
    "likes": ["music", "football"]
  }, 
  {
    "name" : "Mary",
    "age" : 30,
    "likes": ["tennis"]
  } 
]
```

The above query shows the response of an `OR` clause on the `users` table. Any record that contains either of the mentioned values in the arrays column qualify for the result.

## Array of JSON Objects

So far we say arrays of primitive data types inside a JSON object. Let us look at the possibility of the JSON record containing an array of JSON objects. This is valid and recognised by BlobCity. A sample JSON and corresponding table after such an insert is shown below.

```
{
  "name": "A's Kitchen",
  "open": "11:00 am",
  "close": "01:00 am",
  "food": [
    {"name": "Waffles", "price": 5.95},
    {"name": "French Toast", "price": 4.50},
    {"name": "Breakfast", "price": 6.95}
  ] 
}
```

| _id | name | open | close | food.name | food.price | 
|-----|------|------|-------|-----------|------------|
| xxx | A's Kitchen | 11:00 am | 01:00 am | Waffles <br/><br/> French Toast <br/><br/> Breakfast | 5.95 <br/><br/> 4.50 <br/><br/> 6.95

It is interesting to see that the insert of such a JSON, seemingly created a sub collection of `food` within the record for `A’s Kitchen` restaurant. It is important to note the food.name and food.price column actually contain 3 sub records for the one primary records. This makes food a complete sub collection within the primary collection, and can be operated on as an independent collection. However because the primary key of `_id` is associated only with the primary collection, the records in the sub collection are strongly associated
with the records of the primary collection. The capabilities of such a sub collection can be seen by the SELECT queries that can be fired on such sub collections.

```
SELECT * FROM s1.restaurants
[
  {
    "name": "A's Kitchen",
    "open": "11:00 am",
    "close": "01:00 am",
    "food": [
        {"name": "Waffles", "price": 5.95},
        {"name": "French Toast", "price": 4.50},
        {"name": "Breakfast", "price": 6.95}
    ] 
  }
]
```

A simple select operation on the collection returns us the original record that was inserted into the collection. If we attempt selecting on the sub collection of food, let us see the behaviour.

```
SELECT food FROM s1.restaurants
[
  {
    "food": [
        {"name": "Waffles", "price": 5.95},
        {"name": "French Toast", "price": 4.50},
        {"name": "Breakfast", "price": 6.95}
    ] 
  }
]
```

The response contains a single record, with only the `food` tag. It is important to note that the contents did not come as three records for the three elements within the sub collection, but got collected into a single record as was the structure of the insert.

{% include links.html %}
