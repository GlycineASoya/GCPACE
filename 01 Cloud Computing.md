# Cloud Computing

## Cloud Compute Engine

* Same as AWS EC2
* Uses security hardenen KVM (Kernel Virtual Machine)
* VMs are charged for a minimum of 1 minute of use
* VMs are billed in 1-second increments in Cloud Platform billing
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

### Instance Groups

* Set of instances that is managed as a **single entity**
  * **Managed** groups - best practice; identical VMs, created using the same template, configuration, can be autoscaled, recreated automatically after a crash, autobalanced
    * Regional - across region
    * Zonal - across zone
  * **Unmanaged** groups - different configuration of the VMs in the group
* Autoscaling
  * CPU utilization
  * monitoring metric
  * load-balancing capacity
  * queue-vased workloads

### Snapshots

* The user must be assigned the `Compute Storage Admin` role

### Images

* Same as AWS AMI
* Image - a Snapshot, that has copy of disk contents
* Custom Images from local environment/data center can be imported via Virtual Disk import tool from `gcloud` CLI (same as AWS CLI)
* Custom Images must be compatible with GCP available OS
* Can be created from:
  * Disk - assigned to a source VM
  * Snapshot
  * Cloud Storage File - browse the bucket the source file is located
  * Another Image - can be taken from the current or other Project
* Image can be assigned to a Family (*optional*)- group of Images
* Can be Depricated - no longer supported - the replacement has to be assigned

### Preemtible VM

* Same as a Spot instance
* Stays up for up to 24 hours
* 30 second warning before shutdown
* Significantly cheaper than normal VM, up to 80%
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

### GPU

* GPU can be attached to the running machine
* GPU must be compatible with CPU
* GPU is **NOT** allowed for the shared memory VMs
* GPU depends on **zone**
* In case of GPU `On host maintenance` is set to `Terminate VM instance`

### Best Practices

* Choose a machine type with the fewest CPU and memory that still meets the requirements
* Use Cloud Console for an ad hoc administration
* Use `gcloud` commands for a repeatable tasks
* Use startup scripts applied to a VM to perform software updates and other startup tasks
* Crucially modified machine images are worth to make a separate machine image
* Choose Preemptible VMs for fault tolerate workload to reduce cost
* Use SSH/RDP to perform **system-level tasks**
* Use Cloud Console, Cloud Shell, Cloud SDK to perform **VM-level tasks**

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
  * Application components:  
    >Application <- Service <- Version <- Instance
    * Service - a single function with complex applications made up of multiple services, i.e. *microservice*. Defined by the source code and configuration file. Any change in code/configuration file creates new Version
  * Application is one per Project
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
  * \>= 1 Nodes
* Default VM type is *n1-standard-1* (1 vCPU, 3.75GB RAM)
* Kubernetes Engine reserves CPU and Memory ahead
* Cluster Health is supported by *eviction policies* - when a resource is consumed beyond the threshold, Kubernetes will start shutting down pods
* Reliability:
  * Deployment - a group of identical pods
  * Replicas - identical pods
