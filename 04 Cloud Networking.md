# Cloud Networking

## Virtual Private Cloud (VPC)

* Global service
* Can be linked to on-prem infrastructure leveraging Internet Protocol Security (IPSec)
* VPC is automatically created once Porject is created
* VPCs are global resources
* *Subnet*, VPC subnetwork, is a Regional resource
* *Shared VPC* can be created as a part of Organization, which hosted in a common Project
* *VPC peering* is designed to interproject connectivity

### Creating VPC Cloud Console

Cloud Console -> VPC -> Create VPC

Options:

* Name
* Description

It shows the Subnets that will be created

Options for custom Subnet:

* Name
* Region
* IP address range (CIDR)
* Private Google access - assigns an external IP address to the VM to get access to Google Service
* Flow logs - logging of network traffic

Options for Dynamic routing:

* Regional - Google Cloud Routers will learn only routes within the region of the Routers
* Global - Google Cloud Routers will learn routes on all subnets in the VPC in the Regions where are the subnets are resides

Options for DNS:

* DNS server policy - a policy that enables DNS name resolution provided by GCP

### Creating VPC Cloud SDK (Shell)

`gcloud compute networks create VPC_NAME --subnet-mode=auto` - creating a VPC in the default Project with automatically generated subnets

`gcloud compute networks create VPC_NAME --subnet-mode=custom` - creating a VPC in the default Project with manually creation subnets in the VPC

`gcloud beta compute networks subnets create SUBNET_NAME --network=VPC_NAME --region=REGION --range=CIDR_IP --enable-private-ip-google-access --enable-flow-logs` - creating a custom subnet, with enabled Private IP Google Access and Flow Logs

### Creating Shared VPC Cloud SDK (Shell)

* *Shared VPC* is an Organizational-level VPC is available in common Project
* The **Shared VPC Admin** role needs to be assinged to an organization member on organizational or folder level. The descriptior is `roles/compute.xpnAdmin`

`gcloud organizations add-iam-policy-binding ORG_ID --member='user:EMAIL' --role="roles/compute.xpnAdmin"` - assinging a **Shared VPC Admin** role to a user on Organizational level in the Org ID, which can be found by `gcloud organizations list`

`gcloud beta resource-manager folders add-iam-policy-binding FOLDER_NAME --member='user:EMAIL' --role="roles/compute.xpnAdmin"` - assiging a **Shared VPC Admin** role to a user on Folder level to a folder, which can be found by `gcloud beta resopurce-manager folders list --organization=ORG_ID`

`gcloud compute shared-vpc enable HOST_PROJECT_ID` - enabling shared VPC feature on Organizational level

`gcloud beta compute shared-vpc enable HOST_PROJECT_ID` - enabling shared VPC feature on Folder level

`gcloud compute shared-vpc associate-projects add SERVICE_PORJECT_ID -host-project HOST_PROJECT_ID` - associating projects with a shared VPC on Organizational level

`gcloud beta compute shared-vpc associate-projects add SERVICE_PROJECT_ID --host-project HOST_PROJECT_ID` - associating projects with a shared VPC on Folder level

`gcloud compute networks peerings create PEERING_NAME --network=NETWORK_A --peer-project=PROJECT_B --peer-network=NETWORK_b --auto-create-routes` - creating a peering between two VPCs, should be executed for both VPCs

`gcloud compute instances create INSTANCE_NAME --subnet SUBNET_NAME --zone ZONE_NAME` - creating instance with the specified subner and zone

### Expanding CIDR and IP address Manipulation

`gcloud compute networks subnet expand-ip-range SUBNET_NAME --prefix-length 16` - expanding subnet by changing the prefix to a new value - 16 therefore the number of hosts is 65536. Cannot be shrunk, i.e. set `--prefix-length 16` instead of `--prefix-length 24`, only `--prefix-length 8`

* Reservation of IP addresses can be done via:
  * Cloud Console
    * Cloud Console -> VPC -> External IP addressess -> Reserve Static Address
  * Cloud SDK (Shell)
    * `gcloud beta compute addresses create RESERVATION_NAME --region=REGION --network-tier=PREMIUM` - creating an address reservation using Google Cloud Global infrastructure as per network-tier
* Types of reservation:
  * Standard - usage of the Internet, costs lower
  * Premium - usage GCloud Global infrastructure, costs higher
* Reserved IP address stays attached until it released

## Cloud Load Balancing

* Same as AWS ELB (Elastic Load Balancing)
* Balances traffic within and across Regions
* Distribute Workloads among servers running an application
* Types of Load Balancers:
  * Global versus regional
    * Global
      * For globally distributed applications
      * HTTP(S) - balances across set of backend instances
      * SSL Proxy - terminates SSL/TLS connections, non-HTTPS traffic
      * TCP Proxy - terminates TCP sessions and then forwards traffic to backend servers
    * Regional
      * Internal TCP/UDP, balances within VMs
      * Network TCP/UDP, balances based on IP protocol, address, port, is used for SSL and TCP, doesn't support SSL proxy and TCP Proxy
  * External versus internal
    * External distributes traffic from the Internet, uses HTTP(S), SSL Proxy, TCP Proxy, Network TCP/UDP
    * Internal distributes traffic inside GCP, uses TCP/UDP LB
  * Traffic type, such HTTP/TCP
    * TCP traffic can use External Global, External Regional, Internal Regional Load Balancing
    * UDP traffic can use External Regional, Internal Regional Load Balancing

### Load Balancer Cloud Console

Cloud Console -> Network Services -> Load Balancing

Options:

* Type
  * HTTP(S)
  * TCP
  * UDP
* Internet Facing or Internal only
* Multiple Regions or Single Region
* Connection Termination
  * Yes (TCP Proxy, SSL Proxy)
  * No (TCP)
* Backend
  * Name
  * Region
  * Network
  * Backends (Instance Groups)
  * Health Check
    * Check Interval - time to execute a check
    * Timeout - time for waiting for a response from the checking target
    * Healthy/Unhealthy threshold - successful/unsuccessful consecutive attempts to decided the resource involced  into load balancing rotation
* Frontend
  * Name
  * Subnet
  * Internal IP configuration (Manual/Ephemeral (Automatic))
  * Ports (Single, Multiple, All)

### Load Balancer Cloud SDK (Shell)

`gcloud compute forwarding-rules create LOAD_BALANCER_NAME --port=PORT --target-pool POOL_NAME` - creating load balancer that listens port PORT and forward the traffic to Pool of Instances (i.e. Instance Group)

`gcloud compute target-pools add-instances POOL_NAME --instances INSTANCE1,INSTANCE2` - adding instances into instance pool (i.e. Instance Group)

## Cloud Armor

* Same as AWS Shield
* It's built on Cloud Load Balancing service
* Features
  * Allow/restrict access on IP address
  * Rules for counting XSS (cross-site scripting) attacks
  * Counting SQL injections
  * L3/L7 rules
  * Allow/restrict access on Geolocation

## Cloud CDN

* Same as AWS CloudFront
* CDN stands for Content Delivery Network
* >90 CDN endpoints
* It's a global service
* Good for static content and global audience

## Cloud Interconnect

* Same as AWS DirectConnect
* Connects existing networks with Google network
* Types of connections:
  * Interconnects
  * Peering
* Partner interconnect - 3rd parties way to connect to GCloud directly

## Cloud DNS

* Same as AWS Route 53
* Managed by Google
* Provides domain name resolution
* Records:
  * A - maps domain name to IPv4 IP address
  * AAAA - maps domain name to IPv6 address
  * CNAME - stores canonical names, which contains alias names of a domain
  * NS - **N**ame **S**erver record, contains address of an authoritative server, that manages the zone information. Added automatically once zone is created
  * SOA - **S**tart **O**f **A**uthority record, that has authoritative information about the zone. Added automatically once zone is created

### Create DNS Managed Zones Cloud Console

Cloud Console -> Network Services -> Cloud DNS -> Create Zone

Options:

* Zone type
  * public - accessible from the Internet. Provides name servers that responds to queries from any source
  * private - accessible from resources in the same project as the zone. Provide name services to GCP resources (VMs, LBs)
* Zone name
* Description
* DNS name - suffix of a DNS name, *example.com*
* *DNSSEC* - flag, public only, provides strong authentication of clients against DNS services, prevents spoofing (client appears to be other client) and cache poisoning (sending incorrect information to update the DNS server)
* Networks - the networks the private zone will be visible to, private only

### Create DNS Managed Zones Cloud SDK (Shell)

`gcloud beta dns managed-zone create ZONE_NAME --description=DESCRIPTION --dns-name=EXAMPLE.COM` - creating public managed DNS zone in domain name EXAMPLE.COM

`gcloud beta dns managed-zone create ZONE_NAME --visibility=private --networks=default --dns-name=EXAMPLE.COM` - creating private managed DNS zone in domain name EXAMPLE.COM with default networks

### Create DNS record Cloud Console

Cloud Console -> Network Services -> Cloud DNS -> select Zone -> add Record Set

Options:

* DNS Name
* Record Type
* TTL - **T**ime **T**o **L**ive in cache
* TTL Unit - can be minutes, seconds, hours, days

### Create DNS record Cloud SDK (Shell)

* Creating requires starting *transaction*

`gcloud dns record-sets transaction start --zone=ZONE_NAME` - start transaction

`gcloud dns record-sets transaction add IP_ADDRESS --name=EXAMPLE.COM. --ttl=SECONDS --type=A --zone=ZONE_NAME` - adding an A record to a zone

`gloud dns record-sets transaction add SERVER1.EXAMPLE.COM. --name=ALIAS.EXAMPLE.COM. --ttl=SECONDS --type=CNAME --zone=ZONE_NAME` - adding a CNAME record to a zone

`gcloud dns record-sets transation execute --zone=ZONE_NAME` - executing adding transaction
