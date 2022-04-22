# Security

## Firewall

* Firewall rules are defined on the network level and used to control the flow of network traffic to VMs
* Comprises:
  * Direction - Ingress/Egress
  * Priority - 0-65535. The lower the higher. Default is 65535
  * Action - Allow/Deny
  * Target - the rule is applied to
  * Source/Destination - applies to Ingress rules
    * Sources can be:
      * IP ranges
      * Instances with particular network tags
      * Instances using a sepcific service account
      * Combination of them
    * Destination:
      * IP ranges only
  * Protocol and port - TCP, UDP, ICMP and port. With no protocol selected the rule applies to all protocols
  * Enforcment status - the rule either enabled or disabled
* Default (implied) rules for instances cannot be deleted, priority 65535, are:
  * Allow Egress to 0.0.0.0/0
  * Deny Ingress from 0.0.0.0/0
* Default network rules, priority 65534, for VPC:
  * Allow Incoming traffic from any VM on the same network
  * Allow Incoming TCP on port 22, SSH
  * Allow Incoming TCP on port 3389, RDP
  * Allow incoming ICMP from any source on the same network

### Creating Firewall rules Cloud SDK (Shell)

`gcloud compute firewall-rules create` - creating a firewall rule

Options:

* `--action`
* `--allow`
* `--description`
* `--destination-ranges`
* `--direction`
* `--network`
* `--priority`
* `--source-ranges`
* `--source-service-accounts`
* `--source-tags`
* `--target-service-accounts`
* `--target-tags`
