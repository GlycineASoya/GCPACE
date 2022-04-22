# Cloud Storage offerings

## Cloud Storage

* Same as S3
* Can spans multiple regions
* Types of buckets:
  * Multi-regional
    * Multi region bucket
    * Redundant across regions and regions, also called *Georedundant* - at least two locations use and are at least 100 miles (160 km) apart
    * Provides >99.99% monthly availability
    * Provides 99.95% service availability SLA
    * Data is replicated in multiple regions
    * Good for accessing content across regions
    * Can be changed to Nearline/Coldline storage object
  * Regional
    * Single region bucket
    * Redundant across zones
    * Provides 99.99% monthly availability
    * Provides 99.9% availability SLA
    * Can be changed to Nearline/Coldline storage object
  * Nearline storage
    * Cheaper than normal Storage
    * Infrequent data access (less than once per month)
    * Provides: 99.95% multiregional availability, 99.99% regional availability
    * Provides: 99.9% multiregional SLA, 99.0% regional SLA
    * Retrieving infoirmation is *paid*, can be done after 30 days
    * Can be changed only to Coldline storage
  * Coldline storage
    * Cheaper than normal Storage and Nearline Storage
    * More Infrequent data access (once per year)
    * Provides: 99.95% multiregional availability, 99.9% regional availability
    * Provides: 99.9% multiregional SLA, 99.0% regional SLA
    * Retrieving information is *paid*, can be done after 90 days
* Buckets are globally available -> Names should be unique
* Buckets can be mounted to Linux/Mac file system using *Cloud Storage Fuse* open source project
* Versioning:
  * Good to keep a history of changes
  * The latest file version is called *live* version
  * When the object is deleted versions are deleted as well

### Cloud Storage Cloud Console

Cloud Console -> Cloud Storage -> Create Bucket

Options:

* Bucket name
* Storage class (Multiregional, regional, Nearline, Coldline)
* Lifecycle policy:
  * Condition options for Lifecycle rule:
    * Age
    * Creation Data
    * Storage Class
    * Newer Version
    * Live State (Archived, Live)
  * Action:
    * Send Object class of an Object to Nearline
    * Send Object class of an Object to Coldline
    * Delete an Object
* Encryption

### Data Manipulation Cloud Storage

* In Cloud Console is possible to move objects between buckets
* Limitations:
  * Folders cannot be moved
  * Move is not an option in pop-up menu of the selected folder
* In Cloud SDK (Shell):
  * `gsutils mb gs://BUCKET_NAME` - bucket creation
  * `gsutils cp LOCAL_OBJECT_LOCATION gs://BUCKET_NAME` - copying local file to the target bucket
  * `gsutils cp gs://BUCKET_NAME LOCAL_LOCATION` - copying bucket object locally
  * `gsutils mv gs://SOURCE_BUCKET/OBJECT gs://DESTINATION_BUCKET/OBJECT` - moving object from one bucket to another

## Local Attached SSD disks

* Data is lost once VM is shutdown or terminated
* Read IOPS/GB: 266-453
* Write IOPS/GB: 186-240

## Persistent Disk

* Same as EBS
* SSD and HDD
  * SSD good for consistent performance for random data access and sequential data access. Costs more. Performance: 30 read IOPS/GB, 30 write IOPS/GB
  * HDD good for storing large amounts of data, performing batch operations. Costs less. Performance: 0.75 read IOPS/GB, 1.5 write IOPS/GB.
* Up to 64TB
* Exists independently from VM
* Can be mounted on multiple VMs to provide **multireader storage**
* Auto encrypting
* Can be *zonal*, cheaper, or *regional*, expensive
* Can be created blank or from snapshot

## Cloud Storage for Firebase

* Same as Cloud Storage
* Good fit for poor network connections
* Communication is secured

## Cloud Firebase

* NFS-based
* Can be mounted Cloud Compute Engine and Cloud Kubernetes
* Prodactive: high IOPS (input-output operations per second)
* High capacity
