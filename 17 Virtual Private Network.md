# Virtual Private Network (VPN)

## VPN Cloud Console

Cloud Console -> Hybrid Connectivity -> VPN

Options:

* Name
* Description
* Google Compute Engine VPN Gateway - terminates VPN connection on GCP side
  * Network
  * Region
  * Static IP address
* Tunnels - other network endpoints in the VPN
  * Name
  * Description
  * IP address of the local VPN gateway
  * Version of Internet Key Exchange (IKE) protocol
  * Shared secret - required during configuring VPN endpoint
* Rounting Options
  * Dynamic - uses BGP to learn new routes in the networks. Cloud Router is required
  * Route-Based - remote (local side) network IP ranges are required to be specified
  * Policy-Based - remote (local side) network IP ranges, local subnetworks the VPN will be used in, local IP ranges

## VPN Cloud SDK (Shell)

`gcloud compute target-vpn-gateways` - subcommands related to GCP side VPN Gateway
`gcloud compute forwarding-rule` - subcommands related to where to forward the traffic from local environment
`gcloud compute vpn-tunnels` - subcommand related to tunnels

`gcloud compute vpn-tunnel create TUNNEL_NAME --peer-address=PEER_ADDRESS_OF_TUNNEL_REMOTE_ENDPOINT --shared-secret=SHARED_SECRET --target-vpn-gateway=TARGET_GATEWAY_VPN_IP` - creating a VPN tunnel that terminates on VPN Gateway

`gcloud compute forwarding-rules create RULE_NAME --TARGET_SPECIFICATION=VPN_GATEWAY` - creating forwarding rule with one of the following targets ([more info](https://cloud.google.com/sdk/gcloud/reference/compute/forwarding-rules/create)):

* `--target-instance`
* `--target-http-proxy`
* `--target-vpn-gateway`
