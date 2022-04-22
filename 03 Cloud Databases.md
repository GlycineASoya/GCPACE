# Cloud Databases

## Relational

### Cloud SQL

* Same as cut AWS RDS
* Automatic Failover
* Replication
* High Availability
* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* Supports MySQL and PSQL
* First Generation Platform:
  * MySQL:
    * MySQL 5.5 and 5.6 versions
    * 16GB RAM
    * 500GB storage
    * No autoscale of storage
* Second Generation Platform:
  * MySQL:
    * MySQL 5.6 and 5.7 versions
    * 416GB RAM
    * Up to 10TB
    * Autoscale of storage
  * PSQL :
    * PostgreSQL 9.6
    * 64 CPU
    * 416GB RAM
    * Up to 10TB
    * Extensions: cubes (analytics processing), hstore (key-value pair in a single value), PostGIS (adds geographic objects)
* Backups:
  * Costs 0.08$/GB/month
* Good for
  * Web applications
  * Business intelligence
  * Ecommerce applications

#### Cloud SQL Cloud Console

Cloud Console -> Cloud SQL

Options:

* MySQL 5.6, 5.7
  * Name
  * Root password
  * Region
  * Zone
* PostgreSQL 9.6

#### Data Manipulation Cloud SQL

* In Cloud Console:
  * Double click on the Cloud SQL Instance
  * Select Export Tab
  * Specify the Target Bucket
* In Cloud SDK (Shell)
  * `gcloud sql instances describe INSTANCE_NAME` - getting a service account name, that can write to the bucket
  * `gsutil acl ch -u SERVICE_ACCOUNT:PERMISSION gs://BUCKET_NAME` - changing permission for a user against target bucket
  * `gcloud sql export sql INSTANCE_NAME gs://BUCKET_NAME/OBJECT --database=DATABASE_NAME` - exporting data (backup) from Cloud SQL instance from the particular database to a bucket in SQL format
  * `gcloud sql export csv INSTANCE_NAME gs://BUCKET_NAME/OBJECT --database=DATABASE_NAME` - exporting data (backup) from Cloud SQL instance from the particular database to a bucket in CSV format
  * `gcloud sql import sql INSTANCE_NAME gs://BUCKET_NAME/SOURCE_OBJECT --database=DATABASE_NAME` - importing data (backup) to Cloud SQL instance to a specific database from a bucket in SQL format

### Cloud Spanner

* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
  * No manual backups
* Same as AWS Aurora
* Relational DB with horizontal scalability of NoSQL
* Good for
  * Globally supply chains
  * Financial services applications
  * Large relational data volumes
  * Globally distributed
  * Consistency and transaction integrity across all servers
* Expensive than Cloud SQL
* Afger instance creation a DB creation is following

#### Cloud Spanner Cloud Console

Cloud Console -> Cloud Spanner

Options:

* Instance name
* Instance ID
* Number of nodes
* Regional/Multiregional deployment

#### Data Manipulation Cloud Spanner

* In Cloud Console only
  * Cloud Console -> Spanner -> select Instance -> select Source data to export/import to
  * Export requires:
    * Cloud Storage Bucket the data will be exported
    * Database to export
    * Region of the Export Job- if the region of Spanner Instance and Export Job is different Network Egress (that goes outside) will be charged
  * Import requires:
    * Source bucket
    * Destination database
    * Region to run an Import Job

### Cloud BigQuery

* Same as AWS Athena
* Managed by GCP
* Requires Data set
* SQL DB
* Provides:
  * Storage tool
  * Query tool
  * Statistical tool
  * Machine Learning analysis tool
* Good for analytics
* *Jobs* kinds:
  * Load data
  * Export data
  * Copy data
  * Query data
* There is its own CLI: `bq`
* Charges for data scanned in queries

#### Data Manipulation Cloud BigQuery

* In Cloud Console
  * Export data
    * Cloud Console -> BigQuery -> Resources -> select Data set with the target Table -> click Export
    * Export to Data Studio or GCS (Storage)
    * Export formats: JSON, CSV, Avro (Apache Data serialization system). Best option for large data is Avro. Avro can be read by Apache Spark, Cloud Dataproc
    * Export compression: None or gzip for CSV, *deflate*, focus on compression, or *snappy*, focus on compression speed, for Avro
  * Import data
    * Cloud Console -> BigQuery -> select Data set -> Create Table
    * Source can be
      * Empty table
      * Google Cloud Storage
      * Upload from local directory
      * Upload from Google Drive
    * Format can be
      * CSV
      * JSON
      * Avro
      * Parquet
      * PRC
      * Cloud Datastore Backup
* In Cloud SDK (Shell)
  * `bq extract --destination_format FORMAT --compression COMPRESSION_TYPE --field_delimeter DELIMETER --print_header BOOLEAN PROJECT_ID:DATASET.TABLE gs://BUCKET/FILENAME` - exporting data from BigQuery
  * `bq load --autodetect --source_format=FORMAT DATASET.TABLE PATH_TO_SOURCE` - importing data to BigQuery from the source. `--autodetect` detects Table schema from the source

## NoSQL

### Cloud Datastore

* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* NoSQL Database
* Document, key-value pair collection, is the main data block
* Supports REST API
* Autoscale of data storage
* Supports SQL-like syntax
* Support indexes
* Support transactions
* Backup
  * Is taken to the bucket, has to be created with `gsutils`: `gsutils mb gs://BUCKET_NAME`
  * `datastore.database.export` permission is required to export data, i.e. creating backups
  * `datastore.database.import` - permission is required to import data
  * Role is **Cloud Datastore Import Export Admin**
* Good for
  * High scalable data
  * Structured information
  * Not well consistent information

#### Cloud Datastore Cloud Console

Cloud Console -> Datastore -> Create an Entry

Options:

* Namespace - way to group entities (similar to schema in relational DB)
* Kind - similar to table in relational DB
* Key - autogenerated numberic key or custom-defined key
* Value types - String, data and time, Boolean, arrays

#### Data Manipulation Cloud Datastore

* Only Cloud SDK (Shell) is available
  * `gcloud datastore export --namespace="(default)" gs://BUCKET_NAME` - exporting entities from a namespace (default is `(default)`) to a bucket. Itcreates a folder in bucket, with nested folder named after date and time of export. The nested folder contains *metadata* file, which named after data and time of export
  * `gcloud datastore import gs://BUCKET_NAME/DATETIME/DATETIME.overall_export_metadata` - importing entities to Cloud Datastore from bucket file of metadata

### Cloud Bigtable

* Same as AWS RedShift
* NoSQL DB
* Similar to Datastore
* Wide-column DB, not Document DB
* Doesn't require schema to structure the data
* Runs in cluster and scales horizontally
* Petabyte scale data warehouse
* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* Good for
  * Consistent, low-latency read/write operations
  * Applications with hugh data volumes
  * Applications with high-velocity ingest of data
* Integrates with:
  * Cloud Storage (S3)
  * Cloud Pub/Sub
  * Cloud Dataflow
  * Cloud Dataproc, a managed Hadoop and Spark service
  * HBase API (Hadoop API)
* There is its own CLI `cbt`, can be installed via `gcloud components install cbt`
  * It requires environmental variable file: `.cbtrc`
  * `cbt createtable TABLE_NAME` - creates table
  * `cbt createfamily TABLE_NAME COLUMN_FAMILY` - creates a column family
  * `cbt read TABLE_NAME` - reads and display rows
  * `cbt ls` - lists tables and columns

#### Cloud Bigtable Cloud Console

Cloud Console -> Bigtable -> Create Instance

Options:

* Instance name
* Instance ID
* Mode
  * Production - min 3 nodes, high-available
  * Development - low-cost instances without replication/high availability
* Type of disks
  * SSD
  * HDD
* Cluster
  * Cluster ID
  * Region
  * Zone
  * Number of nodes

#### Data Manipulation Cloud Bigtable

* Export and Import is not support via Cloud Console or `gcloud`
* Available options:
  * Java application - the Java application has to be downloaded and in the running `java -jar` command need to be specified
    * Project by `project_id`
    * Table by `table_id`
    * Bucket
    * Zone of the Dataflow job
    * Number of workers
  * HBase commands (modeled after Bigtable)

### Cloud Firestore

* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
  * Provides automatic failover
* NoSQL
* Highly scalable
* Good fit for web and mobile applications
* Datastore mode:
  * Enables written information to be read Cloud Firebase (Cloud Storage Offering)
* Native mode:
  * Provides real-time data sync and offline support
* Support transactions, like relational DB

#### Cloud Firestore Cloud Console

Cloud Console -> Firestroe

Options:

* Data storage system:
  * Datastore mode
  * Native mode - best practice
* Location for the database

## Cache

### Cloud MemoryStore

* Same as AWS ElasticCache
* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
  * Provides automatic failover
* Based on Redis (in-memory database)
* Redis version 3.2
* Memory range: 1GB to 300GB
* High availability
* Good with
  * Compute Engine
  * App Engine
  * Kubernetes Engine
* Types:
  * Basic - doesn't include replica, costs less than Standard
  * Standard - includes failover replica in a separate zone

#### MemoryStore Cloud Console

Cloud Console -> MemoryStore

Options:

* Region
* Zone
* Memory to dedicate
