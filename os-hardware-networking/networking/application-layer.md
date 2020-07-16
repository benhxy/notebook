# Application layer (layer 7)

## DNS (Domain name service)
* To find out the mapping between a domain name and IP address.
* Device uses a DNS server to resolve domain names.
* DNS is a L7 protocol on UDP/IP.

## DHCP (Dynamic host configuration protocol)
* Host creates an IP broadcast to request DHCP information (discovery).
* DHCP servers offer information in unicast response (lease offer).
* Host choose a DHCP server response and request for more information (lease request).
* DHCP server acknowledge the request and assign IP address and other things (acknowledge).
* DHCP is a L7 protocol on UDP/IP.