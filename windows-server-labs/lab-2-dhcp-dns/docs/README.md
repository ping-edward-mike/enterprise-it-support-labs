# Windows Server Lab 2
## Configure DHCP and DNS on Win2k22-DC-01

---

## Lab Overview

This lab builds on **Lab 1** and configures **Dynamic Host Configuration Protocol (DHCP)** and **Domain Name System (DNS)** services directly on the **Domain Controller (`Win2k22-DC-01`)**.

By the end of this lab, domain clients will:
- Automatically receive IP addresses from DHCP.
- Resolve domain resources via DNS.

---

## 🎯 Objectives

1. Install and configure the DHCP role on the Domain Controller (`Win2k22-DC-01`).
2. Create and activate a DHCP scope.
3. Verify that DNS supports Active Directory domain name resolution.
4. Create a Windows 11 client virtual machine (`Win11-01`).
5. Install Windows 11 and join the client to the `ine.local` domain.
6. Test client connectivity and DHCP/DNS functionality.

---

## DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP configuration to client devices, reducing manual setup and ensuring consistent network settings across the domain.

### DHCP DORA Process

DHCP uses a four-step process known as **DORA** to assign IP addresses:

- **Discover** – The client broadcasts a request to locate a DHCP server.
- **Offer** – The DHCP server responds with an available IP address.
- **Request** – The client requests the offered IP address.
- **Acknowledge** – The server confirms the lease and provides configuration details.

### Windows Server DHCP Attributes

| DHCP Attribute | Purpose |
|------|------|
| **Name** (*mandatory*) | Identifies the DHCP scope for administrative reference. |
| **IP Address Range** (*mandatory*) | Defines the pool of IP addresses available for clients. |
| **Subnet Mask / Netmask** (*mandatory*) | Determines the network and host portions of an IP address. |
| **Exclusion** | Reserves specific IP addresses so they are not assigned by DHCP. |
| **Delay** | Controls response priority when multiple DHCP servers exist. |
| **Lease Duration** | Specifies how long an IP address is leased to a client. |
| **Options** | Provides additional settings such as gateway, DNS, and domain name. |
| **Activation** | Enables the scope to begin assigning IP addresses. |

---

## Network Configuration

### Virtual Switch Setup

- **Virtual Switch Name:** `private switch lab`
- **Switch Type:** Private
- **Purpose:**
  - Isolated internal network
  - Communication only between virtual machines
  - No external internet access

---

## DHCP Implementation

### Install DHCP Role

On the Domain Controller:

1. Open **Server Manager**
2. Go to **Add Roles and Features**
3. Select **DHCP Server**
4. Complete the installation
5. Run the **Post-Deployment Configuration**
   - Authorise the DHCP server in Active Directory

![DHCP role installed on Win2k22-DC-01](/windows-server-labs/lab-2-dhcp-dns/screenshots/installed-dhcp-on-win2k22-dc-01.PNG)

---

### Configure DHCP Scope

1. Open **Tools > DHCP**
2. Expand the server node
3. Right-click **IPv4** → **New Scope**
4. Configure the scope with appropriate values:
   - IP address range
   - Subnet mask
   - Default gateway (if applicable)
   - DNS server (Domain Controller IP)
5. Activate the scope

![DHCP scope](/windows-server-labs/lab-2-dhcp-dns/screenshots/dhcp-scope.PNG)
![DHCP scope range](/windows-server-labs/lab-2-dhcp-dns/screenshots/dhcp-ip-ranges.PNG)
![DHCP exclusion addresses](/windows-server-labs/lab-2-dhcp-dns/screenshots/dhcp-exclusion-ips.PNG)
![DHCP configured](/windows-server-labs/lab-2-dhcp-dns/screenshots/dhcp-done.PNG)

---

## DNS Configuration

### DNS Role Overview

DNS was installed during **Lab 1** as part of Active Directory Domain Services.

---

### Verify DNS Configuration

1. Open **Tools > DNS**
2. Expand the server node
3. Confirm the following exist:
   - Forward Lookup Zone: `ine.local`
   - Required records (A, NS, SOA)
4. Ensure DNS is listening on the Domain Controller’s static IP address

---

### DNS Integration with DHCP

- DHCP is configured to:
  - Automatically register client records in DNS
  - Use the Domain Controller as the primary DNS server

This ensures client machines can resolve domain resources correctly.

---

## Client Machine Deployment

### Create Windows 11 Virtual Machine

- **VM Name:** `Win11-01`
- **Operating System:** Windows 11
- **Network Adapter:** `private switch lab`

![Win11-01 VM created](/windows-server-labs/lab-2-dhcp-dns/screenshots/Win11-01-VM-created.jpg)

---

### Install Windows 11 and Join Domain

1. Complete the Windows 11 installation
2. Rename the computer to `Win11-01`
3. Join the domain:
   - Domain name: `ine.local`
4. Restart the machine when prompted
5. Log in using a domain account created in Active Directory
6. Set network configuration to **DHCP**
7. Verify the machine receives:
   - IP address
   - DNS server
   - Default gateway (if configured)

![Win11-01 DHCP working](/windows-server-labs/lab-2-dhcp-dns/screenshots/Win11-01-dhcp-working.PNG)

---

## Validation & Testing

- Client successfully receives an IP address from DHCP
- Client resolves domain names via DNS
- Domain login works on `Win11-01`
- DHCP lease is visible in the DHCP console
- DNS records are created automatically for the client

---

## References

- Microsoft Documentation: Install and Configure DHCP  
  https://learn.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top

- Microsoft Documentation: Configure DNS for Active Directory  
  https://learn.microsoft.com/en-us/windows-server/identity/dns/active-directory-integrated-dns-overview

---

### Next Lab

**Lab 3: Active Directory Basics (OUs, Users, Groups, and Group Policy)**
