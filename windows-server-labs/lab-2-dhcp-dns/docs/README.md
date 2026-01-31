# Windows Server Lab 2
## Configure DHCP and DNS on the Domain Controller

---

## Lab Overview
This lab builds on **Lab 1** and configures **Dynamic Host Configuration Protocol (DHCP)** and **Domain Name System (DNS)** services directly on the **Domain Controller (`Win2k22-DC-01`)**.  

By the end of this lab, domain clients will:  
- Automatically receive IP addresses from DHCP.  
- Resolve domain resources via DNS.  

---

## 🎯 Objectives
By completing this lab, you will be able to:  
1. Install and configure the DHCP role on the Domain Controller.  
2. Create and activate a DHCP scope.  
3. Verify that DNS supports Active Directory domain name resolution. 
4. Create a new VM Win11-01 for Client
5. install a Windows 11 OS for Win11-01 and join Client to domain `ine.local`
6. Test client connectivity and DHCP/DNS functionality.  

---

## DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP configuration to client devices, reducing manual setup and ensuring consistent network settings across the domain.

| Property | Purpose |
|------|------|
| **Name** (*mandatory*) | Identifies the DHCP scope for administrative reference. |
| **IP Address Range** (*mandatory*) | Defines the pool of IP addresses available for clients. |
| **Subnet Mask / Netmask** (*mandatory*) | Determines the network and host portions of an IP address. |
| **Exclusion** | Reserves specific IP addresses so they are not assigned by DHCP. |
| **Delay** | Controls response priority when multiple DHCP servers exist. |
| **Lease Duration** | Specifies how long an IP address is leased to a client. |
| **Options** | Provides additional settings such as gateway, DNS, and domain name. |
| **Activation** | Enables the scope to begin assigning IP addresses. |

## Implementations and Configurations

---

## References
- [Microsoft Documentations : Install and Configure DHCP](https://learn.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top)  
- [Microsoft Documentations : Configure DNS for Active Directory](https://learn.microsoft.com/en-us/windows-server/identity/dns/active-directory-integrated-dns-overview)  
