# DesX Zolutions Ltd – Network Design & Implementation

## Overview

This project presents the network design and implementation for DesX Zolutions Ltd,
a growing architectural design company with approximately 160 employees across
five departments.

The network was designed and implemented using Cisco Packet Tracer.

The implementation includes:

- IP addressing and VLSM
- OSPF routing
- DHCP
- DNS
- HTTP/HTTPS web server
- Email server
- AAA/RADIUS authentication
- Extended ACLs
- Zone-Based Firewall (ZBF)
- Wireless Access Points
- External/ISP connectivity
- Network security zones

## Network Architecture

The network uses a hierarchical star topology consisting of:

- Department Router
- Central Router
- Server Router
- ISP Provider Router
- Department switches
- Wireless Access Points
- Servers
- End-user PCs and laptops

The network is divided into four security zones:

1. Internal
2. DMZ
3. Conference
4. External

## Departments

The internal network contains the following departments:

| Department | Hosts | Network | Subnet |
|---|---:|---|---|
| Design | 55 | 192.168.10.0/26 | 255.255.255.192 |
| Project Management | 40 | 192.168.10.64/26 | 255.255.255.192 |
| Finance | 30 | 192.168.10.128/27 | 255.255.255.224 |
| HR | 25 | 192.168.10.160/27 | 255.255.255.224 |
| IT | 10 | 192.168.10.192/28 | 255.255.255.240 |

## Server Network

The server network uses:

`192.168.10.208/28`

The following services are implemented:

| Service | IP Address |
|---|---|
| Web Server | 192.168.10.210 |
| DHCP Server | 192.168.10.213 |
| AAA/RADIUS Server | 192.168.10.214 |
| DNS Server | 192.168.10.x |
| Email Server | 192.168.10.212 |


## Routing

### OSPF

OSPF is configured between the:

- Department Router
- Central Router
- Server Router

OSPF allows the routers to dynamically learn and update routes.

The network uses OSPF rather than RIP because the design is intended to support
future growth.


## DHCP

DHCP is provided centrally by the DHCP server.

The DHCP server automatically provides clients with:

- IP address
- Subnet mask
- Default gateway
- DNS server

`ip helper-address` is configured on the relevant router interfaces so that
DHCP requests can reach the DHCP server across different subnets.

## DNS

The DNS service provides the domain:

`desxzolutions.com`

The domain resolves to the company's web server.

This allows users to access the website using a domain name rather than directly
entering the server IP address.

## Web Server

The network includes an HTTP/HTTPS web server.

The web server provides the company website and supports:

- HTTP
- HTTPS

The website can be accessed using:

`http://desxzolutions.com`

or

`https://desxzolutions.com`

## Email

An email server is configured using:

- SMTP
- POP3

Users are provided with individual email accounts using the
`desxzolutions.com` domain.

## Wireless Network

Each department has its own Wireless Access Point.

Wireless security is configured using:

- WPA2-PSK
- Unique passwords for each access point

Wireless clients can connect using laptops equipped with the appropriate
wireless module.

## Network Security

### Router Security

The routers are configured with:

- Hostnames
- Encrypted enable passwords
- Console authentication
- VTY authentication
- Password encryption
- Login warning banners
- Local administrator backup accounts

### AAA / RADIUS

AAA authentication is implemented using a RADIUS server.

The AAA server provides centralised authentication for:

- Department Router
- Central Router
- Server Router

A local administrator account is retained as a backup in case AAA
authentication becomes unavailable.

## Access Control Lists

Extended ACLs are used to control communication between departments.

The ACL configuration allows specific departments to communicate with other
departments while restricting unauthorised access.

IT is provided with broader access for administrative purposes.

DHCP and required server traffic are also permitted through the appropriate
ACL rules.

## Zone-Based Firewall

The network is divided into four security zones:

### Internal

Contains:

- Design
- Project Management
- Finance
- HR
- IT

### DMZ

Contains:

- Web Server
- DNS Server
- Email Server
- DHCP Server
- AAA Server

### Conference

Contains the conference room devices and wireless clients.

### External

Represents the simulated ISP/internet network.

Zone pairs and policy maps are used to control traffic between these zones.

## External Connectivity

External connectivity is simulated using:

`8.10.1.0/24`

The ISP Provider uses:

`8.10.1.1/24`

The Central Router uses:

`8.10.1.2/24`

Default routes are configured so that traffic can be forwarded between the
internal network and the simulated ISP.

## Testing

The following network functionality was tested:

- Inter-department communication
- DHCP address allocation
- DNS resolution
- HTTP/HTTPS access
- Email communication
- AAA authentication
- Wireless connectivity
- ACL restrictions
- ZBF restrictions
- External connectivity

Testing confirmed that authorised traffic was permitted while restricted
traffic was blocked.

## Security Zones and Access Summary

| Source | Destination | Access |
|---|---|---|
| Internal | DMZ | Permitted services |
| Internal | Conference | Controlled |
| Conference | Internal | Controlled |
| Conference | DMZ | Web/services |
| External | Internal | Restricted |
| External | DMZ | Controlled |
| IT | Departments | Administrative access |

## Known Limitations

The current design has several limitations:

- The Central Router represents a single point of failure.
- NAT has not been fully implemented.
- VLAN segmentation could be added.
- Backup routers could be introduced for redundancy.
- VPN could be implemented for remote access.
- IPSec could be introduced for additional confidentiality and authentication.

## Troubleshooting

During implementation, DHCP initially failed because the required UDP ports
67 and 68 were not permitted through the extended ACL.

Issues were also encountered when implementing the Zone-Based Firewall.
Incorrect `drop` and `pass` policies affected DHCP and AAA authentication.

These issues were resolved by adding the appropriate protocols to the
class-maps and correcting the policy-map configuration.


## Future Improvements

Potential future improvements include:

1. VLAN segmentation
2. NAT
3. Redundant routers
4. VPN access
5. IPSec
6. Additional firewall controls
7. Improved password policies
8. Increased network redundancy
