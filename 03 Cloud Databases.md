# Cloud Databases

## Cloud SQL

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

## Cloud Bigtable

* Same as AWS RedShift
* Petabyte scale data warehouse
* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* NoSQL DB
* Good for low-latency read/write operations
* Integrates with:
  * Cloud Storage (S3)
  * Cloud Pub/Sub
  * Cloud Dataflow
  * Cloud Dataproc, a managed Hadoop and Spark service
  * HBase API (Hadoop API)

## Cloud Spanner

* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* Same as AWS Aurora
* Relational DB with horizontal scalability of NoSQL

## Cloud Datastore

* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
* NoSQL Database
* Document or key-value pair collection is the main data block
* Supports REST API
* Autoscale of data storage
* Supports SQL-like syntax
* Support indexes
* Support transactions
* Good for
  * High scalable data
  * Structured information
  * Not well consistent information

## Cloud Memorystore

* Same as AWS ElasticCache
* Managed by GCP:
  * No DBA tasks
  * No patching underlying software
  * Provides automatic failover
* Based on Redis (in-memory database)

## Cloud Firestore

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
