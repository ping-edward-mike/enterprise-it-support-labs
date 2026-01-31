# Windows Server Lab 1  
## Domain Foundation & Active Directory Deployment

---

## Lab Overview

This lab established the **Domain Foundation & Active Directory Deployment** for a small enterprise Windows environment.  
It focused on deploying Windows Server 2022, configuring Active Directory Domain Services (AD DS), and preparing the environment for centralized authentication and management.

This lab served as the **base for all subsequent Windows Server and MD-102 labs**.

> ⚠️ DHCP and DNS configuration were intentionally excluded from this lab and were implemented in **Lab 2**.

---

## Lab Objectives

- Deployed Windows Server 2022 virtual machines
- Designed and applied a static IP addressing scheme
- Installed and configured Active Directory Domain Services
- Created a new Active Directory forest and domain
- Joined member servers to the domain
- Established a stable enterprise-ready foundation

---

## Lab Architecture

The lab consisted of three Windows Server virtual machines:

| VM Name | Role | Operating System |
|------|----|----|
| `Win2k22-DC-01` | Domain Controller | Windows Server 2022 Datacenter (Desktop Experience) |
| `Win2k22-SRVR-01` | Member Server | Windows Server 2022 Datacenter |
| `Win2k22-Core-01` | Server Core (Member) | Windows Server 2022 Datacenter (Core) |

---

## Network Design

### Network Addressing

| Setting | Value |
|------|------|
| Network Address | `192.168.10.0/24` |
| Subnet Mask | `255.255.255.0` |
| Usable IP Range | `192.168.10.1 – 192.168.10.254` |
| Default Gateway | `192.168.10.254` |
| Total usable IP addresses | 254 (before allocation) |

---

### Server IP Allocation

| Server | Role | IP Address |
|------|----|----|
| `Win2k22-DC-01` | Domain Controller | `192.168.10.10` |
| `Win2k22-SRVR-01` | Member Server | `192.168.10.20` |
| `Win2k22-Core-01` | Server Core | `192.168.10.30` |

> IP addresses were deliberately spaced to allow for future expansion (additional servers, services, and appliances).

---

## Virtual Switch Configuration

- All virtual machines were initially connected to the **Default External Switch**, providing:
  - Internet connectivity
  - Windows Update access
- The environment was transitioned to an **Internal virtual switch** in **Lab 2** when DHCP was introduced.

---

## Virtual Machine Configuration

### 1. Create Virtual Machines

Three VMs were created with the following names:

- `Win2k22-DC-01`
- `Win2k22-SRVR-01`
- `Win2k22-Core-01`

*VM names matched OS hostnames to simplify administration and troubleshooting.*

![Hyper-V-Manager-with-3-VMs-running](/windows-server-labs/lab-1-setup-environment/screenshots/Hyper-V-Manager-with-3-VMs-running.jpg)

---

### 2. Configure `Win2k22-DC-01`

#### Operating System
- Installed **Windows Server 2022 Datacenter Evaluation**
- Selected **Desktop Experience**

#### Network Configuration
- Configured a **static IPv4 address**:
  - IP Address: `192.168.10.10`
  - Subnet Mask: `255.255.255.0`
  - Default Gateway: `192.168.10.254`
  - Preferred DNS: `192.168.10.10`

#### System Configuration
- Renamed the server to: **`Win2k22-DC-01`**
- Added a system description identifying it as the **Primary Domain Controller**

*Win2k22-DC-01 was renamed and configured with it's static IP address.*

![Win2k22-DC-01-static-ip-config-renamed](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-DC-01-renamed-and-static-ip-configured.PNG)

- Network configuration was verified using `ipconfig /all`.

![Win2k22-DC-01-ipconfig-verify-neytwork-config](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-DC-01-ipconfig-all-to-verify-network-configurations.PNG)

---

## Active Directory Configuration

### 3. Install Active Directory Domain Services (AD DS)

On `Win2k22-DC-01`:

- Installed the **Active Directory Domain Services** role
- Promoted the server to a Domain Controller
- Created a **new forest**
- The domain name was configured as: `ine.local`

---

### 4. Configure `Win2k22-SRVR-01`

- Renamed the server to: **`Win2k22-SRVR-01`**
- Added a system description identifying it as the **Member Server**

#### Network Configuration
- Configured a **static IPv4 address**:
  - IP Address: `192.168.10.20`
  - Subnet Mask: `255.255.255.0`
  - Default Gateway: `192.168.10.254`
  - Preferred DNS: `192.168.10.10`

*Win2k22-SRVR-01 was renamed and configured with it's static IP address.*

![Win2k22-SRVR-01-static-ip-config-renamed](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-SRVR-renamed-and-static-ip-configured.PNG)

- Network configuration was verified using `ipconfig /all`.

![Win2k22-SRVR-01-ipconfig-verify-neytwork-config](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-SRVR-01-ipconfig-all-to-verify-network-configurations.PNG)

---

### 5. Configure `Win2k22-Core-01`

- Renamed the server to: **`Win2k22-Core-01`**

#### Network Configuration
- Configured a **static IPv4 address**:
  - IP Address: `192.168.10.30`
  - Subnet Mask: `255.255.255.0`
  - Default Gateway: `192.168.10.254`
  - Preferred DNS: `192.168.10.10`

*Win2k22-Core-01 was renamed and configured with it's static IP address.*

![Win2k22-Core-01-static-ip-config-renamed-1](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-Core-01-renamed-and-static-ip-configured-1.jpg)

![Win2k22-Core-01-static-ip-config-renamed-2](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-Core-01-renamed-and-static-ip-configured-2.jpg)

---

## Domain Membership

The following servers were joined to the `ine.local` domain:

- `Win2k22-SRVR-01`
- `Win2k22-Core-01`

This validated:

- Network connectivity
- DNS resolution
- Active Directory authentication

---

## Validation and Verification

The following checks were performed to validate the environment:

- Verified domain membership using `systeminfo` and `whoami /fqdn`
- Confirmed DNS resolution between domain members
- Verified secure channel with the domain controller

---

## Deliverables

- One Active Directory forest and domain (`ine.local`)
- One Domain Controller
- Two domain-joined member servers
- Static IP addressing applied consistently for all three servers

---

## References

- Microsoft Documentation: Install Active Directory Domain Services  
  https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-

---

### Next Lab: [**Lab 2 (Configure DHCP and DNS services for the domain)**](/windows-server-labs/lab-2-dhcp-dns/docs/README.md)  
