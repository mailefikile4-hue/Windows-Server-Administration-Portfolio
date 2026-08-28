# Windows Server Administration Portfolio

## Overview

This repository contains my practical lab work for the **Computer Servers' Administration (CSA427E)** module. I'm building this out as I go through the module, so it documents real, hands-on work — setting up virtual machines, standing up a domain from scratch, configuring core infrastructure services, and troubleshooting the things that inevitably break along the way.

Everything here was done in my own virtual lab, built on Hyper-V, running a simulated small enterprise environment for a fictional organization called **CUTHealth**.

## Technologies and Skills

* Windows Server
* Hyper-V Virtualization
* Active Directory Domain Services
* DNS
* DHCP
* Organizational Units
* User and Group Management
* Group Policy
* File and Storage Services
* File Server Resource Manager
* DFS
* Storage Spaces
* Windows Performance Monitoring
* Backup and Disaster Recovery
* Network Troubleshooting
* Azure Integration

---

# Lab Environment

I built this environment from the ground up in Hyper-V, so before anything else in this portfolio could happen, I first had to get the virtualization layer working.

### Current Environment

| Device       | Role                                          | IP Address       |
| ------------ | ---------------------------------------------- | ---------------- |
| DC1          | Domain Controller / DNS                       | 192.168.20.10    |
| DHCP2VM      | DHCP Server / Secondary Infrastructure Server | To be configured |
| Client VM    | Domain Client                                 | DHCP / Static    |
| Hyper-V Host | Virtualization Host                           | Host Environment |

### Active Directory Domain

```text
CUTHealth.ac.za
```

### Network

```text
Network: 192.168.20.0/24

Domain Controller / DNS
DC1
192.168.20.10
```

---

# Portfolio Projects

## 01 – Hyper-V Virtualization

Everything in this portfolio runs on top of Hyper-V, so this is where I started. Before I could build a domain, DNS, or DHCP, I needed a working virtual environment to build them in.

### Practical Activities

* Installing the Hyper-V role
* Creating and configuring virtual switches
* Creating virtual machines for the domain controller and infrastructure server
* Configuring virtual hard disks
* Creating differencing disks
* Allocating and managing VM resources (CPU, RAM, storage)

### Lab Layout

```text
Hyper-V Host
│
├── DCVM
│   └── Windows Server
│       └── DC1
│
└── DHCP2VM
    └── Windows Server
        └── DHCP Infrastructure
```

---

## 02 – Server Fundamentals

Before diving into configuration, I spent time getting my head around what a server actually is and how server infrastructure is typically designed — this grounded everything that came after.

### Skills Demonstrated

* Understanding server roles
* Physical versus virtual servers
* Server operating systems
* Server architecture
* Virtualization concepts

---

## 03 – Active Directory Domain Services

With the VMs up and running, the next step was turning DC1 into an actual domain controller and standing up the CUTHealth.ac.za domain.

### Practical Activities

* Examining workgroup membership
* Configuring server IP settings
* Preparing the server for AD DS installation
* Installing Active Directory Domain Services
* Promoting the server to a Domain Controller
* Creating the CUTHealth.ac.za domain
* Verifying DNS records
* Creating Organizational Units
* Creating domain users
* Creating security groups
* Managing computer accounts
* Examining NTDS and SYSVOL
* Exploring the Global Catalog

### Organizational Structure

```text
CUTHealth.ac.za
│
├── Admin
│   ├── User Accounts
│   └── Administrative Resources
│
├── Clinical
│   └── Clinical Users
│
├── Research
│   └── Research Users
│
└── IT-Support
    └── IT-Support Security Group
```

---

## 04 – Network Infrastructure Services (DHCP & DNS)

With a domain in place, the next logical step was getting the network services running so clients could actually get IP addresses and resolve names properly.

### DHCP

* Installing the DHCP Server role
* Authorizing the DHCP server in AD DS
* Creating a DHCP scope
* Configuring DHCP options
* Managing address leases
* DHCP high availability and failover

### DNS

* Installing DNS
* Managing Forward Lookup Zones
* Managing Reverse Lookup Zones
* Creating and testing DNS records
* Performing name resolution tests

### Verification Commands

```powershell
ipconfig /all
nslookup CUTHealth.ac.za
ping DC1.CUTHealth.ac.za
```

---

## 05 – Storage and File Servers

This is where I set up shared storage for the organization and put some real management controls in place — quotas, file screening, and redundancy through DFS.

### Practical Activities

* Disk Management
* Resource Monitoring
* File Server Resource Manager
* Quotas
* File Screens
* Storage Spaces
* Data Deduplication
* DFS Namespaces
* DFS Replication
* Azure File Sync

---

## 06 – Print Servers

Centralized printing setup — small in scope, but a common real-world admin task.

### Skills Demonstrated

* Installing print services
* Adding printers
* Managing print queues
* Configuring printer sharing
* Managing printer permissions

---

## 07 – Backup and Disaster Recovery

Once there was actually something worth losing, I moved on to making sure it couldn't be lost — backup planning and recovery testing.

### Skills Demonstrated

* Backup planning
* Server backup
* Data recovery
* System recovery
* Disaster recovery planning

---

## 08 – Security and Administration

Locking down the environment — access control, permissions, and policy enforcement.

### Skills Demonstrated

* User authentication
* Group-based access control
* Organizational Units
* Group Policy
* Permissions management
* Security configuration

---

## 09 – Monitoring and Troubleshooting

Every lab in this portfolio eventually broke in some way, and this is the toolkit I used to figure out why and fix it.

### Tools Used

* Task Manager
* Resource Monitor
* Performance Monitor
* Event Viewer
* Command Prompt
* PowerShell

### Example Verification Commands

```powershell
ipconfig /all
nslookup
ping
gpupdate /force
gpresult /r
whoami
hostname
```

---

## 10 – Azure Integration

Finally, extending the on-prem environment into Azure to see how a hybrid setup works in practice.

### Areas Covered

* Azure Virtual Machines
* Windows Server and Azure integration
* Azure file services
* Hybrid infrastructure concepts

---

# Verification Methodology

I tried to keep every project consistent, following roughly the same process each time:

1. Configure the required server role or service.
2. Capture screenshots of the configuration.
3. Test the configuration.
4. Record verification commands and results.
5. Document any problems encountered.
6. Apply troubleshooting procedures.
7. Verify that the problem has been resolved.

---

# Evidence

Each project folder follows this structure:

```text
Project/
│
├── README.md
│
└── Screenshots/
    ├── 01-Initial-Configuration.png
    ├── 02-Role-Installation.png
    ├── 03-Configuration.png
    ├── 04-Verification.png
    └── 05-Troubleshooting.png
```

---

# Skills Demonstrated

* Hyper-V Virtualization
* Windows Server Administration
* Active Directory Administration
* DNS Administration
* DHCP Administration
* User and Group Management
* Organizational Unit Design
* Group Policy
* Storage Management
* File Server Administration
* Server Monitoring
* Troubleshooting
* Backup and Recovery
* Enterprise Infrastructure Design

---

## Author

Advanced Diploma in Computer Networking Student
Aspiring IT Support and Systems Administrator

This repository is a working portfolio — it grows as I move through the module, and reflects real configuration work, real errors, and real fixes rather than a polished textbook walkthrough.
