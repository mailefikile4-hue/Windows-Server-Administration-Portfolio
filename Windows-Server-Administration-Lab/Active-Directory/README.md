# Active Directory Administration

## Overview

This lab documents my practical experience configuring and administering **Active Directory Domain Services (AD DS)** on **Windows Server 2025** using a Hyper-V virtual lab environment.

The lab focuses on creating a domain environment, managing users and groups, organizing users with Organizational Units (OUs), applying Group Policy, and configuring file access permissions.

---

## Lab Environment

| Component         | Configuration       |
| ----------------- | ------------------- |
| Operating System  | Windows Server 2025 |
| Virtualization    | Hyper-V             |
| Domain Controller | DC1                 |
| Domain            | CUTHealth.ac.za     |
| DC1 IP Address    | 192.168.20.10       |
| Subnet Mask       | 255.255.255.0       |
| DNS Server        | 192.168.20.10       |

---

# 1. Configure the Server

The Windows Server was configured with a static IPv4 address and an appropriate computer name before installing Active Directory.

### Configuration

```text
Computer Name: DC1
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
DNS Server: 192.168.20.10
```

### Why?

A domain controller requires reliable network configuration so that clients can consistently locate the domain controller and DNS services.

### Evidence

![Server Network Configuration](./screenshots/01-network-configuration.png)

---

# 2. Install Active Directory Domain Services

The **Active Directory Domain Services (AD DS)** role was installed using Server Manager.

### Steps

1. Open **Server Manager**.
2. Select **Manage**.
3. Select **Add Roles and Features**.
4. Select **Role-based or feature-based installation**.
5. Select the server.
6. Select **Active Directory Domain Services**.
7. Add the required features.
8. Complete the installation.

### Why?

AD DS provides the central directory service used to manage users, computers, groups, authentication and other domain resources.

### Evidence

![AD DS Installation](./screenshots/02-ad-ds-installed.png)

---

# 3. Promote the Server to Domain Controller

After installing AD DS, the server was promoted to a domain controller.

### Domain

```text
CUTHealth.ac.za
```

### Steps

1. Open **Server Manager**.
2. Select the notification flag.
3. Select **Promote this server to a domain controller**.
4. Select **Add a new forest**.
5. Enter:

```text
CUTHealth.ac.za
```

6. Configure the domain controller options.
7. Set the Directory Services Restore Mode password.
8. Complete the prerequisite check.
9. Click **Install**.
10. Allow the server to restart.

### Why?

Promotion changes the Windows Server into a domain controller that can authenticate users and provide Active Directory services.

### Evidence

![Domain Controller](./screenshots/03-domain-controller.png)

---

# 4. Verify the Domain Controller

After restarting, the domain controller was verified using Windows administration tools and command-line utilities.

### Commands

```powershell
ipconfig /all
```

```powershell
whoami
```

```powershell
nslookup CUTHealth.ac.za
```

```powershell
ping 192.168.20.10
```

### Expected Result

The server should resolve the domain and communicate successfully with the domain controller.

### Evidence

![Domain Verification](./screenshots/04-domain-verification.png)

---

# 5. Create Organizational Units

The following Organizational Units were created:

```text
CUTHealth.ac.za
│
├── Admin
├── Clinical
└── Research
```

### Steps

1. Open **Server Manager**.
2. Open **Tools**.
3. Select **Active Directory Users and Computers**.
4. Right-click the domain.
5. Select **New → Organizational Unit**.
6. Create:

```text
Admin
Clinical
Research
```

### Why?

OUs provide a structured way to organize users and computers. They also allow Group Policies to be applied to specific departments.

### Evidence

![Organizational Units](./screenshots/05-organizational-units.png)

---

# 6. Create User Accounts

User accounts were created inside the appropriate departmental OUs.

### User Structure

```text
Admin
├── Admin User 1
└── Admin User 2

Clinical
└── Clinical User

Research
└── Research User
```

### Why?

Creating separate domain accounts allows users to authenticate individually and enables administrators to control access to resources.

### Evidence

![User Accounts](./screenshots/06-user-accounts.png)

---

# 7. Create IT-Support Security Group

An **IT-Support** security group was created for users who require IT-related permissions.

### Steps

1. Open **Active Directory Users and Computers**.
2. Right-click the appropriate location.
3. Select **New → Group**.
4. Enter:

```text
IT-Support
```

5. Select **Security** as the group type.
6. Add the required users.

### Why?

Security groups allow permissions to be assigned to a group rather than configuring permissions individually for every user.

### Evidence

![IT Support Group](./screenshots/07-it-support-group.png)

---

# 8. Configure Group Policy

A **Starter GPO** was created and used as part of the Group Policy administration exercise.

### Steps

1. Open **Server Manager**.
2. Select **Tools**.
3. Open **Group Policy Management**.
4. Locate the domain.
5. Create/configure the required Starter GPO.
6. Link the appropriate policy to the required OU/domain.

### Why?

Group Policy allows administrators to centrally manage Windows settings for users and computers in a domain.

### Verification

```powershell
gpupdate /force
```

```powershell
gpresult /r
```

### Evidence

![Group Policy](./screenshots/08-group-policy.png)

---

# 9. Configure File Permissions

Departmental folders were created to practise access control.

Example:

```text
C:\DepartmentFiles
│
├── Admin
├── Clinical
└── Research
```

Permissions were configured so that users could access the resources appropriate to their department.

### Example Test

The Clinical user was tested to verify that:

* The Clinical folder could be accessed.
* The Admin folder could not be accessed.

### Why?

NTFS permissions help protect files from unauthorized access and ensure that users only access resources they are permitted to use.

### Evidence

![File Permissions](./screenshots/09-file-permissions.png)

![Access Test](./screenshots/10-access-test.png)

---

# 10. Active Directory Verification Commands

The following commands were used during the lab:

### Display IP configuration

```powershell
ipconfig /all
```

### Test network connectivity

```powershell
ping 192.168.20.10
```

### Test DNS resolution

```powershell
nslookup CUTHealth.ac.za
```

### Display current user

```powershell
whoami
```

### Update Group Policy

```powershell
gpupdate /force
```

### View applied Group Policy

```powershell
gpresult /r
```

---

# Skills Demonstrated

Through this practical lab, I developed experience with:

* Windows Server 2025 administration
* Hyper-V virtual machines
* Active Directory Domain Services
* Domain Controller deployment
* Domain configuration
* DNS configuration
* Organizational Units
* User account management
* Security groups
* Group Policy
* NTFS file permissions
* Access control
* Basic Windows Server troubleshooting
* PowerShell and Command Prompt verification

---

# Lab Evidence

Screenshots showing the configuration and testing steps are stored in the:

```text
screenshots/
```

folder.

---

# Conclusion

This lab provided practical experience in deploying and administering a Windows Server Active Directory environment. I configured a domain controller, created departmental OUs and users, created a security group, configured Group Policy, and tested resource access permissions.

The lab demonstrates practical foundational skills in **Windows Server and Active Directory administration**.
