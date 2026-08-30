# Unit 2 – Server Fundamentals and Windows Server Administration

## Project Overview

This project covers the fundamental concepts of computer server administration and introduces the Windows Server environment.

The purpose of this unit was to understand server hardware, server operating systems, server roles, physical and virtual servers, and the basic administration tools used to manage Windows Server.

This unit provides the foundation for later practical projects involving Active Directory, DNS, DHCP, storage, Group Policy, and other Windows Server services.

---

# Lab Environment

The practical environment uses Microsoft Hyper-V to run Windows Server virtual machines.

The server infrastructure created for this portfolio includes:

| Virtual Machine | Server Name | Role                              |
| --------------- | ----------- | --------------------------------- |
| DCVM            | DC1         | Domain Controller                 |
| DCVM            | DC1         | DNS Server                        |
| DCVM            | DC1         | Primary DHCP Server               |
| DHCP2VM         | DHCP2       | Secondary DHCP / Failover Partner |

The virtual machines are connected through a Hyper-V virtual network.

---

# Understanding Servers

A server is a computer that provides services, resources, or functionality to other computers on a network.

The computers that request services from a server are known as clients.

A server can provide services such as:

* User authentication
* File sharing
* DNS name resolution
* DHCP IP address allocation
* Print services
* Application hosting
* Database services
* Virtualization

---

# Client-Server Architecture

A client-server environment allows multiple computers to access centralized services.

```text
                         SERVER
                            │
                  Provides Network Services
                            │
            ┌───────────────┼───────────────┐
            │               │               │
            ▼               ▼               ▼
         Client 1        Client 2        Client 3
```

The server receives requests from clients and provides the required service or resource.

---

# Types of Servers

Different server roles perform different functions within an organisation.

| Server Type           | Function                                                          |
| --------------------- | ----------------------------------------------------------------- |
| Domain Controller     | Provides centralized authentication and Active Directory services |
| DNS Server            | Resolves names to IP addresses                                    |
| DHCP Server           | Automatically assigns IP addresses and network settings           |
| File Server           | Stores and manages shared files                                   |
| Print Server          | Manages network printers                                          |
| Web Server            | Hosts websites and web applications                               |
| Database Server       | Stores and manages databases                                      |
| Application Server    | Provides applications to users                                    |
| Virtualization Server | Hosts and manages virtual machines                                |

A single Windows Server can provide multiple server roles depending on the needs of the organisation.

---

# Windows Server

Windows Server is a server operating system designed to provide centralized services and administration tools for organisations.

Windows Server supports roles and features that can be installed as required.

Examples include:

```text
Windows Server
│
├── Active Directory Domain Services
├── DNS Server
├── DHCP Server
├── File and Storage Services
├── Hyper-V
├── Print and Document Services
└── Web Server
```

Server roles allow one Windows Server installation to perform specific functions within the network infrastructure.

---

# Server Manager

Server Manager is the central administration tool used to manage Windows Server.

It can be used to:

* Add server roles and features
* Monitor server status
* Manage local and remote servers
* Access administrative tools
* Configure server services
* Review events and alerts

## Evidence

```text
Screenshots/01-Server-Manager.png
```

---

# Server Roles and Features

Windows Server uses roles and features to provide specific services.

Roles represent major server functions.

Examples include:

* Active Directory Domain Services
* DNS Server
* DHCP Server
* Hyper-V
* File and Storage Services

Features provide additional functionality that supports server administration and services.

Roles and features can be installed through:

```text
Server Manager
        │
        ▼
Manage
        │
        ▼
Add Roles and Features
```

## Evidence

```text
Screenshots/02-Add-Roles-and-Features.png
```

---

# Physical Servers

A physical server is a dedicated computer containing physical hardware resources.

Typical server hardware includes:

* Processor
* Memory
* Storage
* Network adapters
* Power supply
* Motherboard

Physical servers can be used directly to host operating systems and services.

```text
┌───────────────────────────────┐
│        PHYSICAL SERVER        │
│                               │
│ CPU                           │
│ RAM                           │
│ Storage                       │
│ Network Adapter               │
│                               │
│ Windows Server                │
└───────────────────────────────┘
```

---

# Virtual Servers

A virtual server is a software-based computer that runs on a physical host using a virtualization platform.

In this lab, Microsoft Hyper-V is used to host virtual machines.

```text
                   Physical Host
                         │
                         ▼
                      Hyper-V
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
             DCVM                DHCP2VM
              │                     │
              ▼                     ▼
             DC1                  DHCP2
```

Each virtual machine has its own:

* Operating system
* Virtual CPU
* Memory
* Virtual storage
* Network adapter
* Server configuration

---

# Physical vs Virtual Servers

| Feature        | Physical Server                         | Virtual Server                   |
| -------------- | --------------------------------------- | -------------------------------- |
| Hardware       | Uses dedicated physical hardware        | Uses virtualized hardware        |
| Deployment     | Requires physical hardware installation | Created using a hypervisor       |
| Resource Usage | Dedicated resources                     | Shares host resources            |
| Scalability    | Hardware changes may be required        | Resources can be adjusted        |
| Cost           | Higher hardware requirements            | Multiple VMs can run on one host |
| Testing        | Requires separate systems               | Easy to create lab environments  |

Virtualization allows organisations to use physical resources more efficiently.

---

# Server Hardware Resources

Servers require resources to run operating systems and services.

The main resources include:

## Processor

The processor handles instructions and processes running on the server.

## Memory

Memory provides temporary working space for the operating system and applications.

## Storage

Storage contains:

* Operating system files
* Applications
* User data
* Server databases
* Configuration files

## Network Adapter

The network adapter allows the server to communicate with other devices.

---

# Basic Server Administration

Basic server administration includes managing the server's:

* Computer name
* IP configuration
* Server roles
* Storage
* Users
* Network settings
* System updates
* Services

Administrative tools can be accessed through:

* Server Manager
* Windows Administrative Tools
* Command Prompt
* PowerShell

---

# Basic Verification Commands

The following commands can be used to verify basic server and network information.

## Check Computer Name

```powershell
hostname
```

## Check IP Configuration

```powershell
ipconfig /all
```

## Check Current User

```powershell
whoami
```

## Test Network Connectivity

```powershell
ping 192.168.20.10
```

These commands help administrators verify that a server is correctly configured and communicating on the network.

---

# Practical Lab Configuration

The Windows Server lab environment is built using the following infrastructure:

```text
                    Hyper-V Host
                         │
                    Virtual Switch
                         │
            ┌────────────┴────────────┐
            │                         │
            ▼                         ▼
      ┌─────────────┐           ┌─────────────┐
      │    DCVM     │           │   DHCP2VM   │
      │             │           │             │
      │    DC1      │◄─────────►│    DHCP2    │
      │             │           │             │
      │ AD DS       │           │ DHCP        │
      │ DNS         │           │ Secondary   │
      │ DHCP Primary│           │ / Failover  │
      └─────────────┘           └─────────────┘
```

The network used for the lab is:

```text
Network: 192.168.20.0/24
```

The primary infrastructure server is configured as:

```text
Server Name: DC1
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
```

---

# Screenshots

The following screenshots should be included as evidence for this project:

```text
Screenshots/
├── 01-Server-Manager.png
├── 02-Add-Roles-and-Features.png
├── 03-Windows-Server-Desktop.png
├── 04-Server-Properties.png
├── 05-IP-Configuration.png
├── 06-Command-Line-Verification.png
└── 07-Lab-Environment.png
```

Only screenshots of actual work completed in the lab should be uploaded.

---

# Skills Demonstrated

This project demonstrates knowledge and practical skills in:

* Windows Server fundamentals
* Server hardware concepts
* Server operating systems
* Client-server architecture
* Physical and virtual server concepts
* Windows Server administration
* Server Manager
* Server roles and features
* Basic network configuration
* Command-line verification
* PowerShell fundamentals
* Virtual lab infrastructure

---

# Results

This unit established the fundamental knowledge required for administering Windows Server environments.

The practical lab environment provides a foundation for the implementation of additional server services, including:

```text
Windows Server Infrastructure
│
├── Active Directory
├── DNS
├── DHCP
├── DHCP Failover
├── Group Policy
├── File and Storage Services
├── Print Services
├── Monitoring
└── Backup and Recovery
```

---

# Key Takeaway

Understanding server fundamentals is essential before deploying enterprise services.

This unit introduced the Windows Server environment, server hardware and software concepts, server roles, client-server architecture, and basic administration tools. These concepts form the foundation for the more advanced Windows Server services implemented in the following units.
