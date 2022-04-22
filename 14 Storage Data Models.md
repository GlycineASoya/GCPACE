# Storage Data Models

## Object: Cloud Storage

* Files are atomic objects
* Objects can be overwritten as whole
* No block read/write of the Object
* Good for
  * Large volumes of data
  * Fine-grained access is not required
  * Archived data
  * Machine Learning data
  * IoT data

## Relational: Cloud SQL, Cloud Spanner, BigQuery

* Frequent data access
* Implies consistency of the data
* Support Data transactions - set of operations that guarantees success/fail
* BigQuery is not suitable for transaction-oriented applications, but works with large numbers of rows and columns

## NoSQL: Datastore, Cloud Firestore, Bigtable

* Doesn't require a fixed structure/schema (schema define what kinds of attributes can be stored)

## Choosing Storage solution

1. Read/Write Patterns
   1. Frequent updates - Cloud SQL
   2. Global frequent update - Cloud Spanner
   3. High rates and large volumes - Bigtable
   4. Read/Write files - Cloud Storage
2. Consistency - user reads the data from DB no matter which server responds
   1. Strong consistency - Cloud SQL, Cloud Spanner
   2. Strong consistency, but less IOPS rate, unstructured data - Cloud Datastore
   3. Eventual consistency - NoSQL DB
3. Transaction Support
   1. Cloud SQL, Cloud Spanner, Cloud Datastore
4. Cost
5. Latency - the time between start and finish of the operation
