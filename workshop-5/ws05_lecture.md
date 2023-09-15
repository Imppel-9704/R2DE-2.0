# Road to Data Engineer - Workshop 5 - Lecture

This chapter we are going to learn about Data Warehouse. Send data to Google BigQuery by using Apache Airflow

## What is Data Warehouse?
Data Warehouse is about where to collect large **Structure Data**. It might use a lot of space to collect data. (mostly might be historical data)
- generally use for data analytics or create data model

## Recap : Technology Stack
Technology for data engineering

![Image](https://drive.google.com/uc?id=1EtyJtTUmFa3tJcFE4Y0uxQYJZfKctQSk)

## Data Warehouse concept
## Denormalization
We can collect all of data e.g. customer data, product data all can be collected in one table. Even it use a lot of space because it will collect redundant copies of data.

![Image](https://drive.google.com/uc?id=1FG6dyHdl0rk_F9ryAMnJJmz7Xq4Ct6FZ)


## Normalization
It's about database design to split the table into many tables for not collecting redundant data, keeping table small. but in order to using data, we have to join data to get the result.

![Image](https://drive.google.com/uc?id=1d3OJc8yUwAUoILQjc2mW06xOKlcLlUR8)

## How to make Denormalize use less space
database system collects data as a row in general. (row-based)
row-based will always write new data into database, results easy-to-collect and work fast in case of editing or removing.

Solution to make Denormalize use less space is about using Columnar Storage / Column-oriented Database
Advantage of using Columar Storage is about value in columns are the same, It can read from stored data. Therefore, No need to collect redundant data

![Image](https://drive.google.com/uc?id=1DCD9j_TriVab0TFMbkXqxXVQL5iQByon)

## What is Data Mart? How difference with Data Warehouse?
Data Mart is mostly database for each business unit.

![Image](https://drive.google.com/uc?id=1sABZ9WxoyEz5LfAYY3jOJAKFzqxcy8XK)

## Table & View
View is about using data that is stored in the table to make virtual table by writing SQL.

How to create VIEW
```
CREATE VIEW vw_customer_purchase
AS
SELECT 
  customer AS customer_name,
  COUNT(*) AS purchase_count,
FROM sales_tables
GROUP BY customer_name
```

How to query from VIEW table
```
SELECT * FROM vw_customer_purchase
```

## Recap : Index & Partitioning
Partitioning is about split data in to small group. For example, Split by date, split by ID.
Index is about co-working with Partition to remember where data is, to access data faster.

![Image](https://drive.google.com/uc?id=1LhwIOCCIKGF-gDH_gmWEVSdNJCLZq4CT)

## Google BigQuery
BigQuery is Serverless data warehouse from Google Cloud Platform
- serverless = no need maintainance or infrastructure
- Support many types of data
- easy to use via Web UI or command line
- Can be connected to many BI tools
- pay as you go!

## BigQuery Concept
Project >> Dataset >> Table

![Image](https://drive.google.com/uc?id=1BzozLgsZOz4RImY2F-NMByhmzj7QP4LU)

## Datatype on BigQuery
1. Numeric
- INT64
- NUMERIC
- FLOAT64

2. Boolean (TRUE/FALSE)
- BOOL : true or false

3. String
- STRING

4. Date-Time (ISO)
- DATE : YYYY-[M]M-[D]D
- DATETIME : YYYY-[M]M-[D]D[(|T)[H]H:[M]M:[S]S[.F]]
- TIME : [H]H:[M]M:[S]S[.F]
- TIMESTAMP : YYYY-[M]M-[D]D[(|T)[H]H:[M]M:[S]S[.F]][Time zone]

## Native vs External Table
- **Native table** is collect data inside BigQuery for read or write performance.
- **External table** is about create table outside BigQuery but it similar to real table such as Cloud Storage, Big Table, Google Drive. Lower performance than native table but have an advantage about data management and moving data.

**Federated Query**
BigQuery can query data from other database in GCP by using command EXTERNAL_QUERY

![Image](https://drive.google.com/uc?id=1P3DOBLanyIbf53BngfBLanMBeTpQ1wC8)

## Pricing
**Analysis pricing**
Calculate from amount of data that is processed by using SQL or scan data 5dollar per TB (Free 1TB per month)

**Storage pricing**
pricing is 0.02dollar per GB (Free 10GB per month) for active storage

**Data Ingestion**
- Batch insert or load set of data into database (many rows in 1 time) (Free)
- Streaming insert or load data for each row (0.01 dollar per 200MB per insert)

## Loading Data into BigQuery
1. Load by using Console (Web UI)
2. Use BQ command (CLI: Command Line Interface)
3. SDK & API