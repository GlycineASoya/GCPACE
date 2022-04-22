# Cloud Dataproc

* Desined for
  * Data manipulation
  * Statistical analysis
  * Machine learning

## Deployment

* Create Cluster
  * Cluster name
  * Region
  * Zona
  * Cluster mode
    * Single Node - development environment
    * Standard - only one master node - in case of failure cluster is unaccessible
    * High Availability - three master
  * Machine Configuration information for the master and worker nodes
  * CPU
  * RAM
  * Disks
  * Preemtible VMs usage is an advanced option
* On the Cluster Jobs can be submitted
  * Spark
  * PySpark
  * SparkR
  * Hive
  * Spark SQL
  * Hadoop

## Data Manipulating Cloud Dataproc

* Available only in Cloud SDK (Shell)
  * `gcloud components install beta` - get access to the beta commands
  * `gcloud beta dataproc cluster export CLUSTER_NAME --destination=PATH_TO_EXPORT_FILE` - exporting Cluster Configuration file from Dataproc to a file
  * `gcloud beta dataproc cluster import SOURCE_FILE` - importing Cluster Configuration file to Dataproc from Source (Bucket)\
