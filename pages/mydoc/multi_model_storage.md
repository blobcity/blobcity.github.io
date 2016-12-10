---
title: Multi-Model Storage
sidebar: mydoc_sidebar
permalink: multi-model-storage.html
folder: mydoc
---

## Using BlobCity with diverse data models

The BlobCity database is a multi-model system. By this we mean the database natively stores and processes multiple data formats. Most databases are able to store and process data in a single format, they may take multiple formats of imports and are able to support multiple formats of export, but the data processing / querying is possible only in a single data format.

The BlobCity database is known for its speciality of being able to store and process multiple data types. This means once can store XML and JSON in a single datastore and fire a single SQL query that scans through XML and JSON records as if they were a homogeneous dataset.

Data Type | Description
----------|----------|
JSON | JSON is an open standard format that uses human-readable text to transmit data objects consistent of attribute-value pairs. <br/>[http://www.json.org](http://www.json.org)
XML | Extensible Markup Language (XML) is a markup language that defines a set of rules for encoding documents in a format that is both humanly readable and machine readable. <br/>[http://www.w3.org/XML/](http://www.w3.org/XML/)
CSV | Comma-separated values (CSV) file stores tabular data (numbers and text) in plain text. Each line of the file is a data record. Each record consists of one or more fields, separated by commas. The use of the comma as a field separator is the source of the name for this file format. <br/>[https://en.wikipedia.org/wiki/Comma-separated_values](https://en.wikipedia.org/wiki/Comma-separated_values)
SQL | Structured Query Language (SQL) is a special purpose programming language designed for managing data held in a relational database management system (RDBMS), or for stream processing in a relational data stream management system (RDSMS). <br/>https://en.wikipedia.org/wiki/SQL
Plain Text | Plain text is the data (e.g. file contents) that represent only characters of readable material but not its graphical representation nor other objects (images, etc.). It may also include a limited number of characters that control simple arrangement of text, such as line breaks or tabulation characters. Plain text is different from formatted text, where style information is included, and from "binary files" in which some portions must be interpreted as binary objects (encoded integers, real numbers, images, etc.) <br/>[https://en.wikipedia.org/wiki/Plain_text](https://en.wikipedia.org/wiki/Plain_text)
{% include links.html %}
