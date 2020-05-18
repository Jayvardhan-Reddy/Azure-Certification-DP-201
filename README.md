# Azure-Certification-DP-201: Designing an Azure Data Solution
Road to Azure Data Engineer Part-II

## Exam Pattern

<img src="images/1.Exam-Pattern.jpg">

### 1. Design Azure Data Storage Solutions (40-45%)

- Recommend an Azure data storage solution based on requiremnets

  - choose the correct data storage solution to meet the technical and business requirements
  - choose the partition distribution type

- Design non-relational cloud data stores

  - design data distribution and partitions
  - design for scale (including multi-region, latency, and throughput)
  - design a solution that uses CosDB, Data Lake Storage Gen2, or Blob storage
  - select the appropriate Cosmos DB API
  - design a disaster recovery strategy
  - design for high availability

- Design relational cloud data stores

  - design data distribution and partitions
  - design for scale (including multi-region, latency,throughput)
  - design a solution that uses SQL Database and Azure Synapse Analytics
  - design a disaster recovery strategy
  - design for high availability

### 2. Design Data Processing Solutions (25-30%)

- Design batch processing solutions

  - design batch processing solutions that use Data Factory and Azure Databricks.
  - identify the optimal data ingestion method for a batch processing solution
  - identify where processing should take place, such as at the source, at the destination, or in transit
  - identify transformation logic to be used in the Mapping Data Flow in Azure Data Factory

- Design real-time processing solutions

  - Design for real-time processing by using Stream Analytics and Azure Databricks
  - design and provision compute resources

### 3. Design for Data Security and Compliance (25-30%)

- Design security for source data access

  - plan for secure endpoints (private/public)
  - choose the appropriate authentication mechanism, such as access keys, shared access signatures (SAS), and Azure Active Directory (Azure AD)

- Design security for data policies and standards

  - design data encryption for data at rest and in transit
  - design for data auditing and data masking
  - design for data privacy and data classification
  - design a data retention policy
  - plan an archiving strategy
  - plan to purge data based on business requirements


## 1. Design Azure Data Storage Solutions

## Azure Storage

### BLOB

- It is also a backbone for creating a storage account that can be used as a Data Lake storage

<img src="images/2.Azure-Blob.jpg">

### CosmosDB

- Globally distributed and elstically scalable database.

#### i) Core (SQL) API

- Default API for Azure Cosmos DB
- Can query heirarchical JSON documents with a SQL-like language
- Uses Javascript's type system, expression evaluation, and function invocation.

#### ii) MongoDB API

- Allows existing MongoDB client SDKs, drivers, and tools to interact with the data transparently, as if they are running against an actual MongoDB database.
- Data is stored in document format, similar to Core (SQL)

#### iii) Cassandra API

- Using Cassandra Query language (CQL), the data will appear to be a partitioned row store.

#### iv) Table API

- The original table API only allows for indexing on the partition and row keys; there are no secondary indexes.
- Storing table data in Cosmos DB automatically indexes all the properties, requires no index management.
- Querying is accomplished by using OData and LINQ queries in code, and the original REST API for GET operations.

#### v) Gremlin API

- Provides a graph based view over the data. Remember that at the lowest level, all data in any Azure Cosmos DB is stored in an ARS format.
- Use a traversal language to query a graph database, and Azure Cosmos DB supports Apache Tinkepop's Gremlin language.

## Analyze the storage decision criteria

<img src="images/3.Azure-Storage-Decision_1.jpg">

## Scenario's to choose different CosmosDB API's

<img src="images/4.Core-SQL-Usecase.jpg">

----

<img src="images/5.Core-SQL-Usecase_1.jpg">

------------------------------------------------------------------------

<img src="images/6. Gremlin-Usecase.jpg">

------------------------------------------------------------------------

<img src="images/7.MongoDB-Usecase.jpg">

    - We are not looking into any relationships so Gremlin is not the right choice
    - Other CosmosDB API's are not used since the existing queries are MongoDB native and there MongoDB is the best fit

------------------------------------------------------------------------

<img src="images/8.Cassandra-Usecase.jpg">

------------------------------------------------------------------------

<img src="images/9.Azure-Table-Usecase.jpg">

------------------------------------------------------------------------

## Request Unit Considerations for CosmosDB

- Item size
- Item indexing
- Item property count
- Indexed properties
- Data consistency
- Query patterns
- Script usage

## CosmosDB Partition Design

<img src="images/10.CosmosDB-Partition-Design.jpg">

- Items are placed into logical partitions by partition key
- Partition keys should generally be based on unique values
- Ideally the partition key should be part of a query to prevent "fan out"
- Logical partitions are mapped to physiccal partitions
- A physical partition always contains atleast one logical partition
- Physical partitions are capped at 10GB
- As physical partitions fill-up they will seamlessly split
- Logical partitions can not be split

------------------------------------------------------------------------

<img src="images/11.CosmosDB-Usecase.jpg">

------------------------------------------------------------------------

<img src="images/12.Azure-Table-VS-Cosmos-Table.jpg">

------------------------------------------------------------------------

<img src="images/13. Azure-Storage.jpg">

------------------------------------------------------------------------

## Azure SQL Database hosting options

<img src="images/14.SQL-Hosting-Options.jpg">

------------------------------------------------------------------------

## SQL Security

<img src="images/15.SQL-Security.jpg">

------------------------------------------------------------------------

## Scenario to choose Azure SQL

<img src="images/16.SQL-Usecase.jpg">

------------------------------------------------------------------------

## Scenario to choose Azure Synapse

<img src="images/17.Synapse-Usecase.jpg">

------------------------------------------------------------------------

## Scenario to choose Azure Data Lake Storage Gen2

<img src="images/18.ADLS-Gen2.jpg">

------------------------------------------------------------------------

## Azure Stream Analytics

<img src="images/19.Stream-Analytics.jpg">

------------------------------------------------------------------------

## Scenario to choose Stream Analytics

<img src="images/20.Stream-Analytics-Usecase.jpg">

## 2. Design Data Processing Solutions

### Components of Big Data architecture

<img src="images/21.BigData-Components.jpg">

### Lambda Architecture

<img src="images/22.Lambda-Architecture.jpg">

- When working with very large data sets, it can take a long time to run the sort of queries that clients need.
- Often require algorithms such as Spark/ Mapreduce that operate in parallel across the entire data set.
- The results are then stored seperately from the raw data and used for querying.
- Drawback to this approach is that it intoduces latency

The lambda architecture, addresses this problem by creating two paths for data flow:
- Batch layer (cold path)
- Speed layer (hot path)

### Kappa Architecture

<img src="images/23.Kappa-Architecture.jpg">

- A drawback to the lambda architecture is its complexity.
- Processign logic appears in two different places - the cold and hot paths - using different frameworks
- This leads to duplicate computation logic and the complexity of managing the architecture for both paths.
- The kappa architecture was proposed by Jay Kreps as an alternative to the lambda architecture.
- All data flows through a single path, using a stream processing system.

### IOT

<img src="images/24.IOT.jpg">

### Batch Processing

<img src="images/24.IOT.jpg">

#### Scenario's to use Batch Processing

- From simple data transformations to a more complete ETL (extract-transform-load) pipeline
- In a big data context, batch processing may operate over very large data sets, where the computation takes significant time.
- One example of batch processing is transforming a large set of flat, semi-structured CSV or JSON files into a schematized and structured format that is ready for further querying.

#### Design considerations for Batch processing

- Data format and encoding
    - When files use an unexpected format or encoding
      - Example is text fields that contain tabs, spaces, or commas that are interpreted as delimeters
    - Data loading and parsing logic must be flexible enough to detect and handle these issues.
    
- Orchestrating time slices
    - Often source data is placed in a folder hierarchy that reflects processsing windows, organized by year, month, day, hour, and so on.
    - Can the downstream processing logic handle out-of-order records?

#### Batch processing Logical components

<img src="images/26.Batch-Processing-Logical-Component.jpg">

#### Batch processing Techmology choices

<img src="images/27.Batch-Processing-Technology-Choices.jpg">

#### Batch processing with Azure Databricks

<img src="images/28.Azure-Databricks.jpg">

- Fast cluster start times, autotermination, autoscaling
- Built-in integration with Azure Blob Storage, ADLS, Azure Synapse, and other services.
- User authentication with Azure Active Directory.
- Web-based notebooks for collaboration and data exploration.
- Supports GPU-rnabled clusters.

#### Usage of Azure Databricks

<img src="images/29.Azure-Databricks-Usage.jpg">

-  To read data from multiple data sources such as Azure Blob Storage, ADLS, Azure Cosmos DB, or SQL DW and turn it into breakthrough insights using spark.



------------------------------------------------------------------------

# Tips to remember, A day prior to the Exam.

| Azure Service | Type of File |
| :---: | :---: |
| Azure CosmosDB | Graph Databases |
| Azure Hbase and HDInsight | Column Family in-memory key-value store |

| Azure Service | Usage |
| :---: | :---: |
| Azure Synapse | Data analytics |
| Azure Search | Search engine databases |
| Azure Timeseries Insights | Time series databases |
| Azure Blob | Object store |
| Azure FileStorage | Shared files |

Azure CosmosDB Usage:

- For Real-Time Customer Experiences
- Telemetry stores for IOT
- Migrate NoSQL apps
