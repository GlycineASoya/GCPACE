# Cloud Computing

## Cloud Compute Engine

* Same as AWS EC2
* Uses security hardenen KVM (Kernel Virtual Machine)
* Each VM is assigned to a Project
* Each VM is assigend to a Zone
* Each VM belongs to a Region based on:
  * Cost
  * Data regulations
  * High Availability
  * Latency
  * Specific hardware
* Uses Machine Types (AWS Instance Types) and Snapshots (AWS AMI)
* Custom Machine Types can be set during creation of VM
  * CPU: up to 64 vCPU
  * Memory: up to 6.5GB per 1 vCPU (max 416GB)
* Can be aggreate into *instance groups*

### Snapshots

* Same as AWS AMI
* Custom images from local environment/data center can be imported via Virtual Disk import tool from `gcloud` CLI (same as AWS CLI)
* Custom images must be compatible with GCP available OS

### Preemtible VM

* Same as a Spot instance
* Stays up for up to 24 hours
* 30 second warning before shutdown
* Significantly cheaper than normal VM
* Good for the applications
  * Short-lived
  * Fault-tolerant

#### Preemtible VM Limitations

* Terminate at **ANY** time
* First 10 mins are free of charge
* Will be terminated within 24 hours
* May not be available at the time, depends on Zones, Regions
* Cannot migrate to a regular VM
* Cannot be automatically restart
* Not covered by any SLA

## Cloud App Engine

* Same as AWS Elastic Beanstalk
* Serverless
* PaaS element
* Standard Environment:
  * Good for
    * Single language runtime
  * First Generation:
    * Python 2.7
    * PHP 5.5
    * Go 1.9
    * Allowed language extension
    * Restricted Network access
    * Not recommended to use
  * Second Generation:
    * Java 8
    * Python 3.7 (Beta)
    * PHP 7.2 (Beta)
    * Node.js 8 (Beta), 10 (Beta)
    * Go 1.11 (Beta)
    * Any language extension
    * Full Network access
    * Best Practices
  * Autoscale:
    * Dynamic (depends on workload)
    * Resident (resident instances run constantly - add, modify, delete is manual)
* Flexible Environment:
  * Good for
    * Multiservice application
    * Containerized services
  * Disadvantage: there is always one container you will be charged for
  * Runs Docker containers
  * Requires more configuration due to Docker containers
  * Possibility to use 3rd party libraries and software
  * Work with background
  * Write to a local disk
  * Native support:
    * Java 8
    * Eclipse Jetty 9
    * Phython 2.7, 3.6
    * Node.js
    * Ruby
    * PHP
    * .NET Core
    * Go
* Cost can be handled daily by setting Budget

## Cloud Functions

* Same as AWS Lambda
* Serverless
* Stateless (Each invocation of Cloud Function doesn't share memory, variable)
* PaaS element
* Atomic action
* Supported languages
  * Node.js 6, 8
  * Python 3.7
* Good for:
  * Short running code
  * Event based execution

## Kubernetes

* Same as AWS EKS
* Good for:
  * Large scale applications
  * High availbility is required
  * High reliability is required
* A container orchestration service
* Allows to run *Microservices* - a collection of services
* It's GCP managed service
* Functions:
  * Load Balancing across Compute Enginer VMs, the Kubernetes cluster is installed on
  * Autoscaling of VMs in the cluster
  * Auto update of the cluster software
  * Node monitoring and helath repair
  * Logging
  * Support for *node pools*, collection of nodes with the same configuration
* Copmrises of
  * Master
  * >=1 Nodes
* Default VM type is *n1-standard-1* (1 vCPU, 3.75GB RAM)
* Kubernetes Engine reserves CPU and Memory ahead
* Cluster Health is supported by *eviction policies* - when a resource is consumed beyond the threshold, Kubernetes will start shutting down pods
* Reliability:
  * Deployment - a group of identical pods
  * Replicas - identical pods
