# Unit 1 – Hyper-V Virtualization Lab

## Project Overview

This project demonstrates the creation and configuration of a Windows Server virtual lab environment using Microsoft Hyper-V.

The purpose of this lab is to create a virtual infrastructure that supports the deployment, configuration, testing, and administration of Windows Server services.

Instead of requiring multiple physical servers, Hyper-V is used to create and manage multiple virtual machines on a single physical host.

The virtual lab environment provides the foundation for the rest of the Windows Server Administration projects.

---

# Lab Environment

The lab environment consists of a physical computer running Hyper-V and multiple Windows Server virtual machines.

## Virtual Machines

| Virtual Machine | Server Name | Primary Role                      |
| --------------- | ----------- | --------------------------------- |
| DCVM            | DC1         | Domain Controller                 |
| DCVM            | DC1         | DNS Server                        |
| DCVM            | DC1         | Primary DHCP Server               |
| DHCP2VM         | DHCP2       | Secondary DHCP / Failover Partner |

---

# Lab Architecture

```text
                         Physical Host
                              │
                              │
                        Microsoft Hyper-V
                              │
                       Virtual Switch
                              │
              ┌───────────────┴───────────────┐
              │                               │
              ▼                               ▼
       ┌─────────────┐                 ┌─────────────┐
       │    DCVM     │                 │   DHCP2VM   │
       │             │                 │             │
       │    DC1      │◄───────────────►│    DHCP2    │
       │             │    DHCP         │             │
       │ AD DS       │    Failover     │ Secondary   │
       │ DNS         │                 │ DHCP Server │
       │ DHCP Primary│                 │             │
       └─────────────┘                 └─────────────┘
```

---

# Objectives

The objectives of this project were to:

1. Configure a Hyper-V virtualization environment.
2. Create a virtual network for communication between virtual machines.
3. Create Windows Server virtual machines.
4. Configure virtual machine hardware resources.
5. Configure virtual hard disks.
6. Understand different virtual hard disk options.
7. Prepare the virtual infrastructure for Windows Server roles.
8. Create a primary and secondary DHCP infrastructure.

---

# 1. Hyper-V Virtualization

Microsoft Hyper-V is a virtualization platform that allows multiple virtual machines to run on a single physical computer.

Each virtual machine functions as an independent computer with its own:

* Operating system
* Virtual processor
* Memory
* Virtual hard disk
* Network adapter
* Server roles and applications

This makes it possible to create an enterprise-style server environment without requiring separate physical machines for every server.

## Evidence

```text
Screenshots/01-Hyper-V-Manager.png
<img width="1919" height="1040" alt="Hyper-V Manager 2" src="https://github.com/user-attachments/assets/34f7b791-60ca-4064-b4d8-6ddec87bd722" />

```

---

# 2. Virtual Switch Configuration

A Hyper-V virtual switch was configured to provide network connectivity between the virtual machines.

The virtual switch allows the servers to communicate with each other through the virtual network.

```text
                    Virtual Switch
                         │
                ┌────────┴────────┐
                │                 │
                ▼                 ▼
              DCVM             DHCP2VM
```

## Purpose

The virtual switch provides the network connection required for:

* Server-to-server communication
* Active Directory services
* DNS name resolution
* DHCP communication
* DHCP failover
* Client connectivity

## Evidence

```text
Screenshots/02-Virtual-Switch.png
<img width="716" height="715" alt="Screenshot 2026-08-28 115215" src="https://github.com/user-attachments/assets/d69ee8fd-8bc0-49d4-b60a-c5c4053e11e1" />

```

---

# 3. Creating the DCVM Virtual Machine

A Windows Server virtual machine named `DCVM` was created.

After the operating system and server configuration, the server was configured with the name:

```text
DC1
```

DC1 serves as the primary infrastructure server in the lab.

## Server Roles

The DC1 server provides:

* Active Directory Domain Services
* DNS Server
* Primary DHCP Server

## Network Configuration

```text
Server Name: DC1
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
Network: 192.168.20.0/24
```

## Purpose

DC1 provides centralized identity, authentication, name resolution, and primary IP address allocation services for the lab environment.

## Evidence

```text
Screenshots/03-DCVM.png
```

---

# 4. Virtual Hard Disk Configuration

A new virtual hard disk was created and attached to the virtual machine.

The virtual hard disk stores:

* Windows Server operating system files
* Active Directory data
* DNS configuration
* DHCP configuration
* Applications
* System files

Virtual hard disks allow each virtual machine to have its own isolated storage environment.

## Evidence

```text
Screenshots/04-Virtual-Hard-Disk.png
```

---

# 5. Creating the DHCP2VM Virtual Machine

A second Windows Server virtual machine named `DHCP2VM` was created.

The server is configured to provide secondary DHCP services.

After server configuration, it can be used as a DHCP failover partner for the primary DHCP service running on DC1.

## Server Role

```text
DHCP Server
Secondary / Failover Partner
```

The DHCP infrastructure is designed as:

```text
                    DHCP Infrastructure

             ┌─────────────────────────────┐
             │                             │
             ▼                             ▼
      ┌─────────────┐               ┌─────────────┐
      │     DC1     │               │    DHCP2    │
      │             │               │             │
      │ DHCP Primary│◄─────────────►│ DHCP Backup │
      │             │    Failover   │             │
      └─────────────┘               └─────────────┘
```

## Purpose

The secondary DHCP server improves availability by supporting the primary DHCP server through DHCP failover.

## Evidence

```text
Screenshots/05-DHCP2VM.png
```

---

# 6. Virtual Machine Hardware Configuration

The virtual machines were configured with virtual hardware resources.

The following resources can be configured in Hyper-V:

| Resource          | Purpose                                 |
| ----------------- | --------------------------------------- |
| Processor         | Provides processing resources to the VM |
| Memory            | Provides RAM for the operating system   |
| Virtual Hard Disk | Provides storage                        |
| Network Adapter   | Connects the VM to the virtual network  |
| DVD Drive         | Used for operating system installation  |

Proper resource allocation ensures that the virtual machines can run efficiently on the Hyper-V host.

## Evidence

```text
Screenshots/06-VM-Settings.png
```

---

# 7. Virtual Hard Disk Types

Hyper-V supports different virtual hard disk configurations.

## New Virtual Hard Disk

A new virtual hard disk is created specifically for a virtual machine.

This was used to create an independent storage environment for the Windows Server virtual machines.

## Existing Virtual Hard Disk

An existing virtual hard disk can be attached to another virtual machine when required.

This can be useful when:

* Moving a virtual machine
* Recovering a virtual machine
* Reusing an existing installation

## Differencing Disk

A differencing disk uses a parent virtual hard disk as its base.

Changes made by the child virtual machine are stored in the differencing disk while the parent disk remains unchanged.

```text
             Parent Virtual Hard Disk
                       │
                       ▼
              Differencing Disk
                       │
                       ▼
             Stores VM Changes
```

This can be useful in lab environments where multiple virtual machines require a similar starting configuration.

---

# 8. Managing Virtual Machines

Hyper-V Manager was used to manage the virtual machines.

Administrative actions include:

* Starting virtual machines
* Shutting down virtual machines
* Connecting to virtual machines
* Configuring VM settings
* Managing memory
* Managing processors
* Managing virtual hard disks
* Configuring network adapters

The status of each virtual machine can be monitored directly through Hyper-V Manager.

## Evidence

```text
Screenshots/07-VMs.png
<img width="1919" height="1040" alt="Hyper-V Manager 2" src="https://github.com/user-attachments/assets/a72521a6-6320-4aad-aec7-3a78b206d1e0" />


```

---

# 9. Network Infrastructure

The virtual machines operate within the following network:

```text
Network Address: 192.168.20.0/24
```

The primary server configuration is:

```text
Server: DC1
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
```

The infrastructure supports communication between:

```text
DC1
 │
 ├── Active Directory
 ├── DNS
 └── Primary DHCP
       │
       │ DHCP Failover
       ▼
     DHCP2
       │
       └── Secondary DHCP
```

---

# 10. Verification

The Hyper-V environment was verified by confirming that:

* Hyper-V Manager was operational.
* The virtual switch was configured.
* DCVM was successfully created.
* DHCP2VM was successfully created.
* Virtual hard disks were attached.
* Virtual network adapters were configured.
* The virtual machines were able to start.

Basic verification commands include:

```powershell
hostname
ipconfig /all
ping 192.168.20.10
```

---

# Screenshots

The following screenshots are included as evidence of the Hyper-V implementation:

```text
Screenshots/
├── 01-Hyper-V-Manager.png
├── 02-Virtual-Switch.png
├── 03-DCVM.png
├── 04-Virtual-Hard-Disk.png
├── 05-DHCP2VM.png
├── 06-VM-Settings.png
└── 07-VMs-Running.png
```

Additional screenshots can be added as the virtual lab environment expands.

---

# Skills Demonstrated

This project demonstrates practical skills in:

* Hyper-V administration
* Windows Server virtualization
* Virtual machine creation
* Virtual machine configuration
* Virtual processor configuration
* Virtual memory configuration
* Virtual hard disk management
* Virtual networking
* Virtual switch configuration
* Differencing disk concepts
* Windows Server infrastructure design
* Primary and secondary DHCP architecture
* DHCP failover concepts

---

# Results

A Hyper-V virtual lab environment was successfully created to support Windows Server infrastructure services.

The environment includes a primary infrastructure server, DC1, and a secondary DHCP server, DHCP2.

```text
                    Hyper-V Infrastructure
                             │
                ┌────────────┴────────────┐
                │                         │
               DC1                      DHCP2
                │                         │
        ┌───────┼────────┐                │
        │       │        │                │
       AD DS    DNS    DHCP Primary ◄─────┘
                              DHCP Failover
```

This virtual infrastructure provides the foundation for the following Windows Server administration projects:

* Active Directory Domain Services
* DNS
* DHCP
* DHCP Failover
* Group Policy
* File and Storage Services
* Windows Server security
* Monitoring and troubleshooting

---

# Key Takeaway

Hyper-V allows administrators to create and manage multiple virtual servers on a single physical host.

This project demonstrates the creation of a virtual Windows Server infrastructure consisting of a primary server, DC1, providing Active Directory, DNS, and primary DHCP services, together with DHCP2 as a secondary DHCP failover partner.

The Hyper-V environment serves as the foundation for the remaining practical projects in this Windows Server Administration portfolio.
