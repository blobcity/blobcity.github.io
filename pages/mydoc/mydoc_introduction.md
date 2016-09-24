---
title: Overview
sidebar: mydoc_sidebar
permalink: mydoc_introduction.html
folder: mydoc
---

## What is BlobCity

BlobCity is a multi-model database designed for real-time and low-latency analytics.

    multi-model = SQL + JSON + XML + CSV + Plain Text

Storing and processing diverse data is made easily possible with BlobCity. Most analytic products today are required to collectively analyse data of diverse natures. BlobCity is designed to offer real-time analytics over your diverse data.

The term multi-model refers to a wide variety of data formats. A product supporting more than one data format is termed multi-model. The formats supported by BlobCity are not exhaustive, but are definitely much more than those supported by other similar databases.

If you read though this chapter, you should be able to pass an interview on BlobCity’s features, uses and advantages. The terms BlobCity, BlobCity DB and BlobCity Database are used interchangeably throughout the book, and mean the same.

## When to use

The BlobCity Database is primarily designed to support analytical requirements of your applications. Use in both real-time and low-latency analytics is best suited. If you need to analyse your transactional data at the speed of every transaction, you need a real-time analytics system. Example case could be ATM fraud detection, where your analytical algorithm needs to analyse possible fraudulent nature of an on-going ATM swipe, before the machine actually dispenses the cash.

Unlike ATM’s not all systems need analytics at real-time. If you want to analyse stock market data of the previous day, compare it with a years trend and then take a position when the market opens next day, you need a system that can perform this analysis with low-latency to be able to complete analytics for all stock quotes before the markets re- open. Depending on the nature and complexity of the requirement, the term low-latency covers processing times from a few milliseconds to even several hours.

The BlobCity database is extremely well suited for such analytical requirements. The product is fully ACID compliant and supports high volume of transactions without compromising on analytics speeds. The technical term for such a product is HTAP (Hybrid Transaction / Analytical Processing)1, whereby products that do real-time analytics, need to be able to handle both transaction and analytical processing, in order to process the real-time data at real-time. BlobCity is a very mature HTAP space and used by several application developers as the only database for their applications, supporting both transactions and analytical workloads.

## Naming Conventions

Data inside BlobCity is collected into “datastore’s" and “collections”. A datastore is at the highest level in the storage system. It does not store any data, but it stores multiple collections within itself. There can be as many datastore as desired, but all uniquely named within a cluster. A collection is the equivalent of a database table. A collection is always placed inside a datastore, and is uniquely named within the datastore. Collection names can be repeated across datastore’s.

In a real-life scenario, all data that corresponds to a single application, or single logical module, should be spread across collections inside a single datastore. That across collections can be collectively queried by using SQL JOIN queries that span across collections, just as they would across tables. A single query however cannot lookup data that is across datastore’s. A datastore is useful, when the same instance of the database is to be used for multiple applications, and a datastore is created for storing the data of each respective application.

The rationale behind such naming, is got to do with BlobCity’s ability to take any and every kind of data. Calling it a database, or a table instead of datastore and collection, would be inappropriate as the terms “database” and “table” have very strongly defined meanings. BlobCity does much more than standard definitions of a database or table.

## High Level Features

BlobCity is a NoSQL distributed horizontally, infinitesimally and linearly scalable database. It is fully ACID compliant and takes concurrent transactional and analytical workloads. It supports data sharding, distributed querying, data replication and automated failover management. The data formats supported are diverse including JSON, XML, CSV, SQL and Plain Text. One can inject data into it, by an explicit insert query, or ask the database to automatically pickup data by monitoring various supported data stores.

The table below covers the features of BlobCity DB at a high level. A comparison is intentionally not provided as part of this book, but the features are indicative of the wide variety of uses of the storage technology that are suitable for both applications that want an easy system, and enterprises that want state of the art security and control.

Feature | Description
--------|-----------|
Storage | Disk, In-memory and In-memory-non-durable.
Storage Engine | Proprietary
Consistency | Strongly consistent
Durability | Highly durable, with synchronous data replication
Querying | JDBC, ODBC, SQL, WebServices
Partitioning Scheme | Automatic node health and load based data distribution
Native Partioning | Yes
Data Replication | Yes. Configurable to desired level of copies
Automatic Replication | Yes
Automatic Failover Management | Yes. No database downtime on single or multiple node failover
Data Formats | Natively supports: 
            | * JSON documents 
            * XML documents 
            * CSV records and documents 
            | * SQL insert statements for data loading • Plain text records * Folder / File watch over text files

## Survey of features

Some of the more prominent features of this theme include the following:

* Bootstrap framework
* [Navgoco multi-level sidebar](http://www.komposta.net/article/navgoco) for table of contents
* Ability to specify different sidebars for different products
* Top navigation bar with drop-down menus
* Notes, tips, and warning information notes
* Tags for alternative navigation
* Advanced landing page layouts from the [Modern Business theme](http://startbootstrap.com/template-overviews/modern-business/).

## Getting started

To get started, see [Getting Started][index].

{% include links.html %}
