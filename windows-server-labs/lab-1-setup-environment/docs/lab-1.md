# Windows Server Lab 1  
## Domain Foundation (Active Directory)

---

## Lab Overview

This lab establishes the **foundational identity infrastructure** for a small enterprise Windows environment.
It focuses on deploying Windows Server 2022, configuring Active Directory Domain Services (AD DS), and preparing the environment for centralized authentication and management.

This lab serves as the **base for all subsequent Windows Server and MD-102 labs**.

> ⚠️ DHCP and DNS configuration are intentionally excluded from this lab and will be implemented in **Lab 2**.

---

## Lab Objectives

- Deploy Windows Server 2022 virtual machines
- Design and apply a static IP addressing scheme
- Install and configure Active Directory Domain Services
- Create a new Active Directory forest and domain
- Join member servers to the domain
- Establish a stable enterprise-ready foundation

---

## Lab Architecture

The lab consists of three Windows Server virtual machines:

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
| Total Useable IP address | `254 (*before assigning any*)` |
---

### Server IP Allocation

| Server | Role | IP Address |
|------|----|----|
| `Win2k22-DC-01` | Domain Controller | `192.168.10.10` |
| `Win2k22-SRVR-01` | Member Server | `192.168.10.20` |
| `Win2k22-Core-01` | Server Core | `192.168.10.30` |

> IP addresses are deliberately spaced to allow for future expansion (additional servers, services, and appliances).

---

## Virtual Switch Configuration

- All virtual machines are initially connected to the **Default External Switch**
- This provides:
  - Internet connectivity
  - Windows Update access
- The environment will transition to an **Internal virtual switch** in **Lab 2** when DHCP is introduced

---

## Virtual Machine Configuration

### 1. Create Virtual Machines

Create three VMs using the following names:

- `Win2k22-DC-01`
- `Win2k22-SRVR-01`
- `Win2k22-Core-01`

VM names match OS hostnames to simplify administration and troubleshooting.

![Hyper-V-Manager-with-3-VMs-running](/windows-server-labs/lab-1-setup-environment/screenshots/Hyper-V-Manager-with-3-VMs-running.jpg)

---

### 2. Configure `Win2k22-DC-01`

#### Operating System
- Install **Windows Server 2022 Datacenter Evaluation**
- Select **Desktop Experience**

#### Network Configuration
- Configure a **static IPv4 address** 
- Set :
  - IP Address : `192.168.10.10`
  - Subnet Mask : `255.255.255.0`
  - Default Gateway : `192.168.10.254`
  - Preferred DNS : `192.168.10.10`

#### System Configuration
- Rename the server to: 

**`Win2k22-DC-01`**

- Add a system description identifying it as the **Primary Domain Controller**

*Win2k22-DC-01 renamed and configured with a static IP address.*

![Win2k22-DC-01-static-ip-config-renamed](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-DC-01-renamed-and-static-ip-configured.PNG)

- Network configuration verified using ipconfig /all.
![Win2k22-DC-01-ipconfig-verify-neytwork-config](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-DC-01-ipconfig-all-to-verify-network-configurations.PNG)

---

## Active Directory Configuration

### 3. Install Active Directory Domain Services (AD DS)

On `Win2k22-DC-01`:

- Install the **Active Directory Domain Services** role
- Promote the server to a Domain Controller
- Create a **new forest**
- Configured the domain name as: ine.local

---

### 4. Configure `Win2k22-SRVR-01`

- Rename the server to : 

**`Win2k22-SRVR-01`**

- Add a system description identifying it as the **Member Server**

#### Network Configuration
- Configure a **static IPv4 address** 
- Set :
  - IP Address : `192.168.10.20`
  - Subnet Mask : `255.255.255.0`
  - Default Gateway : `192.168.10.254`
  - Preferred DNS : `192.168.10.10`

*Win2k22-SRVR-01 renamed and configured with a static IP address*

![Win2k22-SRVR-01-static-ip-config-renamed](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-SRVR-renamed-and-static-ip-configured.PNG)

- Network configuration verified using ipconfig /all.
![Win2k22-SRVR-01-ipconfig-verify-neytwork-config](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-SRVR-01-ipconfig-all-to-verify-network-configurations.PNG)

---

### 5. Configure `Win2k22-Core-01`

- Rename the server to : 

**`Win2k22-Core-01`**

#### Network Configuration
- Configure a **static IPv4 address** 
- Set :
  - IP Address : `192.168.10.30`
  - Subnet Mask : `255.255.255.0`
  - Default Gateway : `192.168.10.254`
  - Preferred DNS : `192.168.10.10`

*Win2k22-Core-01 renamed and configured with a static IP address*

![Win2k22-Core-01-static-ip-config-renamed-1](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-Core-01-renamed-and-static-ip-configured-1.jpg)

![Win2k22-Core-01-static-ip-config-renamed-2](/windows-server-labs/lab-1-setup-environment/screenshots/Win2k22-Core-01-renamed-and-static-ip-configured-2.jpg)


---

## Domain Membership

The following servers were joined to the `ine.local` domain:
- `Win2k22-SRVR-01`
- `Win2k22-Core-01`

This validates :
- Network connectivity
- DNS resolution
- Active Directory authentication

---

## Lab 1 Deliverables

- One Active Directory forest and domain (`ine.local`)
- One Domain Controller
- Two domain-joined member servers
- Static IP addressing applied consistently for all three servers

---

### Next - Lab 2 : (DNS & DHCP Services)
