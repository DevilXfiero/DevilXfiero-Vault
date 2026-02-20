
# Ch-1 Trade-offs in Data System Architecture

- Store data so that they, or another application, can find it again later (_databases_)

- Remember the result of an expensive operation, to speed up reads (_caches_)

- Allow users to search data by keyword or filter it in various ways (_search indexes_)

- Handle events and data changes as soon as they occur (_stream processing_)

- Periodically crunch a large amount of accumulated data (_batch processing_)

The application code is often _stateless_ (i.e., when it finishes handling one HTTP request, it forgets everything about that request)

## Analytical versus Operational Systems

- _Operational systems_ consist of the backend services and data infrastructure where data is created, for example by serving external users. Here, the application code both reads and modifies the data in its databases, based on the actions performed by the users.

- _Analytical systems_ serve the needs of business analysts and data scientists. They contain a read-only copy of the data from the operational systems, and they are optimized for the types of data processing that are needed for analytics.

_transaction_ nevertheless stuck, referring to a group of reads and writes that form a logical unit.

An operational system typically looks up a small number of records by some key (this is called a _point query_). Records are inserted, updated, or deleted based on the user’s input. Because these applications are interactive, this access pattern became known as _online transaction processing_ (OLTP).

In order to differentiate this pattern of using databases from transaction processing, it has been called _online analytic processing_ (OLAP).

|Property|Operational systems (OLTP)|Analytical systems (OLAP)|
|---|---|---|
|Main read pattern|Point queries (fetch individual records by key)|Aggregate over large number of records|
|Main write pattern|Create, update, and delete individual records|Bulk import (ETL) or event stream|
|Human user example|End user of web/mobile application|Internal analyst, for decision support|
|Machine use example|Checking if an action is authorized|Detecting fraud/abuse patterns|
|Type of queries|Fixed set of queries, predefined by application|Analyst can make arbitrary queries|
|Data represents|Latest state of data (current point in time)|History of events that happened over time|
|Dataset size|Gigabytes to terabytes|Terabytes to petabytes|
### Data Warehousing

It is usually undesirable for business analysts and data scientists to directly query these OLTP systems, for several reasons:

- the data of interest may be spread across multiple operational systems, making it difficult to combine those datasets in a single query (a problem known as _data silos_);

- the kinds of schemas and data layouts that are good for OLTP are less well suited for analytics (see [“Stars and Snowflakes: Schemas for Analytics”](https://learning.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/ch03.html#sec_datamodels_analytics));

- analytic queries can be quite expensive, and running them on an OLTP database would impact the performance for other users; and

- the OLTP systems might reside in a separate network that users are not allowed direct access to for security or compliance reasons.
Data Warehouse - Seperate database form OLTP db.


This process of getting data into the data warehouse is known as _Extract–Transform–Load_ (ETL)

Extract from Db,
Transform as required,
Load to data warehouse


Some database systems offer _hybrid transactional/analytic processing_ (HTAP)

### Data Lake

 _data lake_: a centralized data repository that holds a copy of any data that might be useful for analysis, obtained from operational systems via ETL processes.
 
The difference from a data warehouse is that a data lake simply contains files, without imposing any particular file format or data model. Files in a data lake might be collections of database records, encoded using a file format such as Avro or Parquet.


Systems of record

A system of record, also known as _source of truth_, holds the authoritative or _canonical_ version of some data. When new data comes in, e.g., as user input, it is first written here. Each fact is represented exactly once. If there is any discrepancy between another system and the system of record, then the value in the system of record is (by definition) the correct one.

Derived data systems

Data in a derived system is the result of taking some existing data from another system and transforming or processing it in some way. If you lose derived data, you can recreate it from the original source. A classic example is a cache: data can be served from the cache if present, but if the cache doesn’t contain what you need, you can fall back to the underlying database. Denormalized values, indexes, materialized views, transformed data representations, and models trained on a dataset also fall into this category.


# Cloud vs Self-hosting

Inhouse or outsourced ? 
Should you build or should you buy ? 

Cloud services are particularly valuable if the load on your systems varies a lot over time.

The term _cloud-native_ is used to describe an architecture that is designed to take advantage of cloud services.