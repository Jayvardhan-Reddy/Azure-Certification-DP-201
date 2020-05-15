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
