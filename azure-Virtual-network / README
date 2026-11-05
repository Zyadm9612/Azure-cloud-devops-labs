# Azure Virtual Network & Subnets – Two-Tier Architecture

## Project Overview
This project demonstrates how to build a two-tier network architecture in Microsoft Azure using Virtual Networks, Subnets, Network Security Groups (NSGs), and Virtual Machines.

## Architecture

- **Web Tier:** Public-facing Ubuntu VM running Nginx.
- **Application Tier:** Private Ubuntu VM with no public IP.
- **Communication:** Private communication between the two VMs over TCP port 8080.

## Azure Resources

| Resource | Configuration |
|---|---|
| Resource Group | `rg-azure-Vnet-lab` |
| Virtual Network | `vnet-production-lab` |
| Address Space | `10.10.0.0/16` |
| Web Subnet | `10.10.1.0/24` |
| App Subnet | `10.10.2.0/24` |
| Web VM | `web-vm` – `10.10.1.4` |
| App VM | `app-vm` – `10.10.2.4` |

## Network Security

**Web NSG (`nsg-web`):**
- Allow HTTP (TCP 80).
- Allow HTTPS (TCP 443).
- Allow SSH (TCP 22) from the authorized IP address.

**Application NSG (`nsg-app`):**
- Allow TCP 8080 from the web subnet.
- Deny inbound traffic from the Internet.

## Implementation & Testing

- Created an Azure Virtual Network with separate web and application subnets.
- Deployed two Ubuntu 24.04 virtual machines.
- Installed and configured Nginx on the web VM.
- Verified public web access through the web VM.
- Tested private connectivity between both VMs.

**Connectivity test results:**
- ICMP ping from `web-vm` to `app-vm`: Successful.
- TCP connection test to port 8080: Connection refused (backend service not yet configured).

## Technologies Used
- Microsoft Azure
- Azure Virtual Network & Subnets
- Network Security Groups
- Ubuntu Server 24.04 LTS
- Nginx
- SSH

## Learning Outcomes
- Understanding Azure networking fundamentals.
- Implementing subnet segmentation.
- Configuring inbound and outbound security rules.
- Understanding public and private VM communication.
- Testing network connectivity using Linux commands.

---

**Status:** Network infrastructure deployed and private VM connectivity verified. Backend application configuration is a future step.
