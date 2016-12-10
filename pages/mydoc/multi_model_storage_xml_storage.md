---
title: XML Storage
sidebar: mydoc_sidebar
permalink: multi-model-storage-xml.html
folder: mydoc
---

## XML Storage

BlobCity offers exhaustive support for XML storage. It allows storage and retrieval of XML, along with running queries on XML as if they were collected into a tabular structure.

A schema inference engine processes the XML document or object being submitted to BlobCity and maps to a tabular schema for appropriate indexing and search-ability. The XML elements are converted to column names, and the values encapsulated within the elements associate with the value of the particular column. Nesting of XML element is permitted with the nested tags forming a column name column name by concatenating the tags separated by a ‘.’ (dot).

Let us consider starting with an empty collection and then insert our first XML document into it. An empty collection is shown in figure below.

```json
{
  "name" : "John",
  "age" : 45 
}
```
The collection after insert of the single JSON record looks as mentioned below.

**Collection with 1st JSON record inserted

_id | 
----| 


{% include links.html %}
