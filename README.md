Corporate Network with DNS/DHCP Services and Internet Access
Subject: Data Networks
Instructor: Ing. Nelson Vera Mendez
Members:

Cecilia Inés Montes Muñoz

Alex David Otero Limones

Bruno Rafael Romero Yagual

David Elias Sandoval Bernitta

Scenario

The simulated corporate network for Tilinsitos S.A. has been designed to manage both internal and external connectivity efficiently and securely. The network is divided into two main subnets: one for the employee LAN and another for the internal server network.

A central router, RED_PRINCIPAL, serves as the heart of the network. This device not only routes traffic between the internal subnets but also connects to a router representing the simulated ISP. To allow internal devices with private IP addresses from the 10.0.0.0/24 network to access the Internet, the router implements NAT overload (PAT).

Within the server network, two essential services are provided:

DHCP: Automatically assigns IP addresses to devices on the employee LAN.

DNS: Resolves both local domain names like servidor.empresa.local and external ones like www.proveedor.com
.

Finally, an external web server simulates the Internet, and an internal web server hosts the company's local website.

Objectives
General Objective

Design, implement, and validate a corporate network with multiple segments, integrating essential network services like DHCP and DNS, and enabling Internet access for internal hosts through NAT configuration on an edge router.

Specific Objectives

Implement a topology with at least two subnets: one for employees and another for servers, with a WAN link connecting them to a simulated ISP router.

Configure a DHCP server to automatically assign IP addresses, subnet masks, default gateways, and DNS servers to employee network devices.

Deploy a DNS service to resolve both internal and external domain names, ensuring that clients can access resources by name instead of by IP address.

Configure network routing and NAT on the edge router to enable internal hosts with private IPs to access external Internet services.

Demonstrate the correct functioning of all services via ping tests, DNS resolution with nslookup, and web access.

Topology

<img width="1179" height="693" alt="image" src="https://github.com/user-attachments/assets/ff47e500-ae50-4942-ba91-71133560d031" />

| Device           | Interface        | IP Address   | Subnet Mask     | Default Gateway |
| ---------------- | ---------------- | ------------ | --------------- | --------------- |
| Laptop 0 (DHCP)  | NIC              | 10.0.0.2     | 255.255.255.128 | 10.0.0.1        |
| Laptop 1 (DHCP)  | NIC              | 10.0.0.3     | 255.255.255.128 | 10.0.0.1        |
| PC 0 (DHCP)      | NIC              | 10.0.0.4     | 255.255.255.128 | 10.0.0.1        |
| PC 1 (DHCP)      | NIC              | 10.0.0.5     | 255.255.255.128 | 10.0.0.1        |
| RED\_PRINCIPAL   | FastEthernet 0/0 | 10.0.0.1     | 255.255.255.128 | NA              |
|                  | FastEthernet 0/1 | 10.0.0.129   | 255.255.255.128 | NA              |
|                  | Serial 0/0/0     | 206.45.160.1 | 255.255.255.252 | NA              |
| ServerDHCP/DNS   | NIC              | 10.0.0.130   | 255.255.255.128 | 10.0.0.129      |
| ServerWebInterno | NIC              | 10.0.0.131   | 255.255.255.128 | 10.0.0.129      |
| ISP              | FastEthernet 0/0 | 206.45.160.5 | 255.255.255.252 | NA              |
|                  | Serial 0/1/0     | 206.45.160.2 | 255.255.255.252 | NA              |
| ServerWebExterno | NIC              | 206.45.160.6 | 255.255.255.252 | 206.45.160.5    |

Configurations
DNS

The configured DNS service resolves local domain names like servidor.empresa.local and external ones like www.proveedor.com
. The domain names are translated to the following IP addresses:

servidor.empresa.local: 10.0.0.131

www.proveedor.com
: 206.45.160.6

DHCP

The DHCP configuration includes the following parameters:

Pool Name: Defines the range of IP addresses that the server can assign.

Default Gateway: The default gateway for employee devices, usually the router interface on the employee subnet.

DNS Server: The IP address of the server used for resolving domain names.

Start IP Address: The starting IP address for the DHCP pool.

Maximum Number of Users: Limits the number of devices that can receive an IP address from the pool.

NAT

The NAT configuration on the RED_PRINCIPAL router includes:

Access List: Defines which internal IP addresses can be translated.

Inside and Outside Interfaces: Specifies the internal and external router interfaces.

PAT Overload: Allows multiple internal devices to share one public IP address for outbound connections.

Evidence
Ping Tests

Laptop0 to RED_PRINCIPAL: Connectivity in the employee network confirmed.

PC0 to RED_PRINCIPAL: Connectivity between employee network and server subnet confirmed.

PC1 to ISP: Internet connectivity confirmed through NAT.

DNS Queries

Laptop1 and PC0 successfully resolved internal and external domain names through the DNS server.

Web Access

PC1 to Internal Web Server: Access to the internal company website confirmed.

PC0 to External Web Server: Successful access to external websites validated via NAT.

Conclusion

The corporate network for Tilinsitos S.A. was successfully implemented, achieving all design and functionality objectives. The following points were validated:

Proper network segmentation for employees and servers.

DHCP configured for automated IP assignment.

DNS functionality validated for both internal and external domains.

NAT configuration confirmed successful external access.

This project demonstrates a complete and functional network solution, integrating vital services like DHCP, DNS, and NAT for efficient and secure operation.
