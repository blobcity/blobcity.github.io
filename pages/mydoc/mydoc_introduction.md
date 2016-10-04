---
title: Overview
sidebar: mydoc_sidebar
permalink: mydoc_introduction.html
folder: mydoc
---

## What is BlobCity?

BlobCity is a multi-model database designed for real-time and low-latency analytics.
{% include callout.html content="multi-model = SQL + JSON + XML + CSV + Plain Text" type="info" %} 

Storing and processing diverse data is made easily possible with BlobCity. Most analytic products today are required to collectively analyse data of diverse natures. BlobCity is designed to offer real-time analytics over your diverse data.

The term multi-model refers to a wide variety of data formats. A product supporting more than one data format is termed multi-model. The formats supported by BlobCity are not exhaustive, but are definitely much more than those supported by other similar databases.

Terms BlobCity, BlobCity DB and BlobCity Database are used interchangeably throughout the documentation, and mean the same.

## When to use

BlobCity Database is primarily designed to support analytical requirements of an application. Use in both real-time and low-latency analytics is best suited. If you need to analyse your transactional data at the speed of every transaction, you need a real-time analytics system. Example case could be ATM fraud detection, where your analytical algorithm needs to analyse possible fraudulent nature of an on-going ATM swipe, before the machine actually dispenses the cash.

Unlike ATM’s not all systems need analytics at real-time. If you want to analyse stock market data of the previous day, compare it with a years trend and then take a position when the market opens next day, you need a system that can perform this analysis with low-latency to be able to complete analytics for all stock quotes before the markets re- open. Depending on the nature and complexity of the requirement, the term low-latency covers processing times from a few milliseconds to even several hours.

The BlobCity database is extremely well suited for such analytical requirements. The product is fully ACID compliant and supports high volume of transactions without compromising on analytics speeds. The technical term for such a product is HTAP (Hybrid Transaction / Analytical Processing)1, whereby products that do real-time analytics, need to be able to handle both transaction and analytical processing, in order to process the real-time data at real-time. BlobCity is a very mature HTAP space and used by several application developers as the only database for their applications, supporting both transactions and analytical workloads.

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
Data Formats | Natively supports: <br/>• JSON documents <br/>• XML documents<br/>• CSV records and documents<br/>• SQL insert statements for data loading<br/>• Plain text records<br/>• Folder / File watch over text files
Indexing | On Disk: BTree, Hashed, Timeseries<br/>In-memory: BTree, Timeseries, Geo-Spatial
Geo-distributed Replication | Yes with configurable consistence. Both strong and delayed consistency supported
Stored Procedures | Java & Scala language support.<br/> <br/>Type of stored procedures:<br/>• Simple Stored Procedures<br/>• Filters for distributed table scans<br/>• Triggers for formulas, data relationships and validations • Map-reduce
Load External Libraries | External Java & Scala libraries loadable for use with stored procedures.
Operating Systems | Linux, Mac OS X, Windows
Hardware Requirements | Runs on commodity hardware. Minimum 4GB RAM and 2 core processor advised.
In-memory Data Cubes | Yes. Proprietary algorithm that provides mathematical complexity of a cube for analytics, along with providing the ability to push operational workloads directly to the cube storage.
Permission & Access Control | Exhaustive user authentication module, with comprehensive roles and privileges. Data access can be controlled all the way down to column level.
Encryption | AES. Configurable number of iterations, and user defined encryption key
Availability | As a hosted multi-tenant database as a service on most major cloud providers, and on-premise or dedicated cloud installations. Tested on Amazon Web Services, Microsoft Azure, Google Cloud Platform, IBM Softlayer, Digital Ocean and Exoscale.
Distribution | [Docker](http://docker.com), [Vagrant](https://www.vagrantup.com/) and OS specific binaries

## Getting started

To get started, see [Getting Started][index].

{% include links.html %}
