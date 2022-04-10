# Cloud Networking

## Virtual Private Cloud (VPC)

* Global service
* Can be linked to on-prem infrastructure leveraging Internet Protocol Security (IPSec)

## Cloud Load Balancing

* Same as AWS ELB (Elastic Load Balancing)
* Balances traffic within and across Regions
* Load balancing
  * HTTP/S
  * TCP/SSL
  * UDP

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
