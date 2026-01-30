# 🧪 Windows Server Lab 1
## Domain Foundation (Active Directory & DNS)

### 📌 Lab Overview
This lab demonstrates the setup of a foundational Windows Server 2022 domain environment using **Active Directory Domain Services (AD DS)** and **DNS**.  
The environment simulates a small enterprise on-premises network and serves as the foundation for all subsequent Windows Server and MD-102 labs.

### 🎯 Objectives
- Deploy Windows Server 2022 virtual machines  
- Configure static IP addressing and DNS  
- Promote a server to Domain Controller  
- Join member servers and a Windows 11 client to the domain  
- Validate domain authentication and name resolution  

### 🧱 Lab Architecture

#### Logical Architecture
![Logical Architecture](diagrams/logical-architecture.png)  
*Replace the above with your lab’s logical architecture diagram.*

#### Network Architecture
![Network Architecture](diagrams/network-architecture.png)  
*Replace the above with your lab’s network diagram.*

### 🖥️ Lab Environment
**Virtualisation Platform:** Hyper-V  

**Operating Systems:**  
- Windows Server 2022 (GUI)  
- Windows Server 2022 Core  
- Windows 11  

### 🧩 Machines & Roles

| Hostname        | Role                                   |
|-----------------|---------------------------------------|
| Win2k22-DC-01   | Domain Controller (AD DS, DNS)        |
| Win2k22-SRVR-01 | Member Server                          |
| Win2k22-Core    | Server Core (Domain Member)            |
| Win11-01        | Domain-joined Client                   |

### 🌐 Network Configuration

| Machine         | IP Address       | DNS Server        |
|-----------------|-----------------|-----------------|
| Win2k22-DC-01   | 192.168.10.10   | 127.0.0.1       |
| Win2k22-SRVR-01 | 192.168.10.20   | 192.168.10.10   |
| Win2k22-Core    | 192.168.10.30   | 192.168.10.10   |
| Win11-01        | DHCP / Static   | 192.168.10.10   |

**Subnet:** 255.255.255.0  
**Domain name:** `ine.local`

### ⚙️ Implementation Steps

1. **Virtual Machine Creation**
   - Created four virtual machines using Hyper-V  
   - Installed operating systems according to assigned roles  

2. **Network & Host Configuration**
   - Assigned static IP addresses to all servers  
   - Configured DNS on all machines to point to `Win2k22-DC-01`  
   - Renamed machines using enterprise naming standards  

3. **Active Directory Deployment**
   - Installed **Active Directory Domain Services** on `Win2k22-DC-01`  
   - Promoted the server to **Domain Controller**  
   - Created a new forest and domain: `ine.local`  
   - Installed DNS during domain promotion  

4. **Domain Join Operations**
   - Joined `Win2k22-SRVR-01` to `ine.local`  
   - Configured `Win2k22-Core` using `sconfig` and joined it to the domain  
   - Joined `Win11-01` to the domain  
   - Verified computer objects appeared in Active Directory  
