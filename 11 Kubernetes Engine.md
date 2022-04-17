# Kubernetes Engine (GKE)

## General information

* One master - manages nodes
* One or more nodes - execute workload
* Users use `kubectl` command to interact with the cluster
* Each node runs an agent called `kubelet` - service that communicates with cluster master
* Machine type can be specified during cluster creation. Default n1-standard-1, 1 vCPU, 3.75GB RAM
* Part of vCPU and RAM is occupied by Kubernetes and not availble for containers:
  * RAM occupied:
    * 25% - 4GB RAM
    * 20% - 4GB-8GB RAM
    * 10% - 8GB-16GB RAM
    * 6% - 112GB-128GB RAM
    * 2% - >128GB RAM
  * vCPU occupied:
    * 6% - 1 Core
    * 1% - 1-2 Cores
    * 0.5% - 2-4 Cores
    * 0.25% - >4 Cores
* Kuberentes are run on container-optimized OS

### Pods

* Pod - *single instance of running process*
* Contain at least one container
* Use shared network and storage across containers
* Each Pod has a unique IP address and ports
* Containers inside Pod can talk with each other on the localhost, but different port
* Pod allows containers inside it to behaev as if they are running on the same VM with shared: storage, IP address, set of ports
* Pod treat multiple containers as a single entity to manage
* Pods create groups - Replicas - copies of pods that manages as a separate unit
* Pods support Autoscaling
* Pods are ephemeral, they are expected to terminate
* Controller manages for Pods Autoscaling and Health monitoring

### Services

* It is an object that provides API endpoint with the stable IP address and indirectly bound with Pods running a particular application
* Update only when changes to Pods are made to get updated list of Pods

### ReplicaSet

* Controller used by a Deployment that ensures correct number of Pods are runnning
* Responsible for recreating the Pods in case of Pods failure
* Responsible for Autoscaling
* Used to update/delete Pods

### Deployment

* It is a set of identical Pods - running the same apploication
* The Pods are identical as the are using the same Pod template - *Pod Specification*
* Good for State*less* applications - don't require to track their state

### StatefulSet

* State*ful* Deployment
* Assing unique identifiers to Pods
* Unique identifiers allow Kubernetes to track which Pod is used by which client
* Good for
  * Unique network identifier applications
  * Stable persistent storage

### Job

* Abstraction of workload
* Job create Pods and run them until workload is complete

### Volumes

* *Persistent volumes* - durable disks are managed by Kubernetes, implemented using Compute Engine peristent disks (same as AWS EBS)
* *Storage class* - type of storage with set of policies fo: quality of service, backup policy, **provisioner** (service to implement the storage)

### Namespaces

## Deployment Kubernetes Cluster

### Deployment GKE Cloud Console

1. Enable Kubernetes Engine API
2. Create credentials for API
3. Create a Kubernetes Cluster from a template - difference with the underlying infarstructe resources - temlates can be adjusted
4. Connection to the cluster is done by `gcloud` prepared command

### Deployment GKE Cloud SDK (Cloud Shell)

*Note. `beta` work could not be used if the service is generally available*

1. `gcloud beta container`
2. `gcloud contianer clusters create CLUSTER_NAME [--num-nodes=NODES_NUMBER] [--region=REGION_NAME]`

## Managing Kubernetes Cluser

### Managing Cluster Cloud Console

Cloud Console -> Kubernetes Engine -> select Cluster -> select Node Pool in Node Pools section -> set Size

### Managing Cluster Cloud SDK (Cloud Shell)

`gcloud container clusters resize CLUSTER_NAME --node-pool NODE_POOL_NAME --size CLUSTER_SIZE` - creates new nodes in the cluster

`gcloud container clusters update CLUSTER_NAME [--enable-autoscaling --min-nodes NUMBER --max-nodes NUMBER] [--node-pool NODE_POOL_NAME]` - update exisiting cluster

## Deployment Application to GKE

### Deployment App Cloud Console

* Fields to specify:
  * Container image
  * Environment variables
  * Initial command
  * App name
  * Labels
  * Namespace
  * Cluster to deploy to
* Returns YAML specification

### Deployment App Cloud SDK (Cloud Shell)

* `gcloud components install kubectl` - installing `kubectl` locally
* `kubectl run DEPLOYMENT_NAME --image=CONTAINER_IMAGE --port=PUBLISHED_PORT` - creating deployment with the target container image
* `kubectl scale deployment DEPLOYMENT_NAME --replicas=DESIRED_REPLICAS_NUMBER` - scaling the existing deployment replicas

## Managing Application to GKE

### Managing App Cloud Console

Cloud Console -> select Workload on the left -> select Deployment -> in Actions choose:

* Autoscale - automatic add/remove replicas depends on CPU utilization
* Expose - exposing service on a port (Port, Target Port, Protocol)
* Rolling Update - rolling update options:
  * Minimum Seconds ready - seconds to wait before considering Pod is updated
  * Maximum Surge - number of Pods above target size allowed
  * Maximum Unavailable - number of unavailable Pods
  * Container name - image
* Scale - set the replicas number

### Managing App Cloud SDK (Cloud Shell)

Managing aplications is done by managing Deployments

`kubectl get deployments` - lists deployments in the chosen namespace
`kubectl scale deployment DEPLOYMENT_NAME --replicas NUMBER` - add/remove replicas
`kubectl autoscale deployment DEPLOYMENT_NAME --min NUMBER --max NUMBER --cpu-percent NUMBER` - autoscaling deployment
`kubectl delete deployment DEPLOYMENT_NAME` - delete deployment

## Managing Services

### Managing Services Cloud Console

Cloud Console -> Kubernetes Engine -> Workloads -> Deploy action -> specify:

* Container image (Google Container Registry URL is the option (`gcr.io/google-samples/hello-app:2.0`))
* Environment variables
* Initial command (optional)
* App name
* Namespace
* Labels
* Cluster

### Managing Services Cloud SDK (Cloud Shell)

`kubectl get services` - lists services in the namespace
`kubectl run SERVER_NAME --image=IMAGE_URL --port PORT` - run the service
`kubectl expose deployment SERVICE_NAME --type="TYPE_OF_SERVICE"` - exposing service to make it accessible to resource *outside the cluster*
`kubectl delete service SERVICE_NAME` - remove a service

## Image Repository

* Google Containter Registry - service for storing container images

### Managing GCR Cloud Console

Cloud Console -> Container Registry

### Managing GCR Cloud SDK (Cloud Shell)

`gcloud container images list [--repository REPOSITORY_URL]` - lits the images
`gcloud container images describe URL_TO_IMAGE` - get extra details of image

## kubectl

NOTE. Configure `kubeconfig` file, which contains information on how to communicate with the API server with the following command:
`gcloud container cluster get-credential [-zone=ZONE_NAME] CLUSTER_NAME`

`kubectl get nodes` - lists the cluster nodes
`kubectl get pods` - lists pods in the chosen namespace
`kubectl describe nodes` - more details about nodes
`kubectl describe pods` - more details about pods
