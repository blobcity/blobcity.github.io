---
title: Simple Stored Procedure Execution
sidebar: mydoc_sidebar
permalink: webservice-simple-stored-procedure.html
folder: mydoc
---

## Simple Stored Procedure Execution

The simple stored procedure can be executed by simply invoking it by its name. The stored procedure needs to be loaded by the given name into the datastore for the operation to be successful. 

```
{
  "username" : "root",
  "password" : "root",
  "ds" : "datastore1",
  "q" : "sp",
  "p" : {
    "name" : "HelloWorld",
    "p" : {
      "param1" : "value1"
    }
   } 
}
```
The name of the stored procedure is specified by the `name` parameter in the payload. The invocation has an optional parameter for a second payload within the primary payload by the name p. The second payload allow you to pass parameters to the stored procedure as a JSON object. This is required for stored procedures that take input parameters for invocation, and is ignored for procedures that do not take any parameters for the invocation.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
  }
}
```
Stored procedures follow a user defined response structure. The database only acknowledges execution of the procedure by a simple `ack` value of `1` and `0`. The stored procedure responds back with a user defined JSON object, which is provided as part of the response within the `p` parameter. A stored procedure may choose to not return any value, in which case the payload in the response will be an empty JSON.


{% include links.html %}
