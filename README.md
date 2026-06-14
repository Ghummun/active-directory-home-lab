# Active Directory Home Lab — Azure

A self-hosted Active Directory environment built on a Windows Server 2022 virtual machine in Microsoft Azure. This project simulates the core responsibilities of an IT help desk or junior sysadmin role: standing up a domain controller, organizing users and computers into Organizational Units, managing security groups, and performing day-to-day account administration tasks like password resets and account enable/disable.

## Project overview

- **Platform:** Microsoft Azure (Free Tier)
- **VM:** `DC01` — Windows Server 2022 Datacenter, Azure Edition Core
- **Resource group:** `AD-Lab`
- **Domain:** `corp.local`
- **NetBIOS name:** `CORP`
- **Roles installed:** Active Directory Domain Services (AD DS), DNS Server, Group Policy Management

## What this project demonstrates

- Deploying and configuring a Windows Server VM in Azure
- Connecting to a remote server via RDP
- Promoting a server to a domain controller and creating a new Active Directory forest
- Designing an OU structure that mirrors a real organization (IT, HR, Finance, Sales)
- Creating user accounts and assigning them to the correct OU
- Creating and managing security groups for department-based access control
- Performing common help desk tasks: password resets, account lockouts, enabling/disabling accounts
- Using Active Directory Administrative Center and Active Directory Users and Computers (ADUC)

## Build walkthrough

### 1. Provisioning the virtual machine

Created a new VM named `DC01` in a dedicated `AD-Lab` resource group, running Windows Server 2022 Datacenter (Azure Edition Core).

![Azure VM creation](screenshots/Azure%20create%20virtual%20Machine%20basics%20tab.png)

### 2. Connecting via RDP

Connected to the server remotely using Remote Desktop Protocol. The VM was restarted at one point during the project, which assigned it a new public IP — both connection prompts are shown below.

![RDP login - first session](screenshots/RDP%20login%20screen.png)
![RDP login - after restart with new IP](screenshots/rdp%20login%20screen%20new%20.png)

### 3. Server Manager — before configuration

Initial Server Manager dashboard on a fresh Windows Server install, before any roles have been added.

![Server Manager dashboard - default](screenshots/server%20manager%20dashboard.png)

### 4. Installing AD DS, DNS, and Group Policy Management

Used the Add Roles and Features Wizard to install Active Directory Domain Services, DNS Server, and Group Policy Management — the core roles required to run a domain controller.

![Add Roles and Features installation](screenshots/add%20roles%20and%20features%20installation.png)

### 5. Server Manager — after configuration

Server Manager now showing AD DS, DNS, and File and Storage Services as active roles on the server.

![Server Manager - roles installed](screenshots/server%20manager%20added%20roles%20screenshot.png)

### 6. Promoting the server to a domain controller

Configured the server as the first domain controller in a new forest. Created the domain `corp.local` with NetBIOS name `CORP`, running at the Windows Server 2025 functional level with Global Catalog and DNS Server enabled.

![AD DS Configuration Wizard - review options](screenshots/Domain%20selection%20screen%20showing%20corp.local.png)

### 7. Building the OU structure

Created an Organizational Unit structure that mirrors a typical company: **IT**, **HR**, **Finance**, and **Sales**. Each department's users and resources live in their own OU, which makes applying Group Policy and delegating permissions much cleaner than dumping everyone into the default Users container.

![OU structure](screenshots/OU%20structure%20active%20directory.png)

### 8. Creating a new user account

Created a new user, **Emily Davis**, in the IT OU — simulating onboarding a new IT department employee.

![New user creation - Emily Davis](screenshots/AD%20project%20user%20creation%20screen.png)
![Setting initial password](screenshots/Password%20creation%20AD.png)

### 9. Resetting a user's password

Performed a password reset for **Sarah Jones** in the HR OU, with "User must change password at next logon" enabled — standard practice for help desk password reset tickets.

![Password reset - Sarah Jones (HR)](screenshots/reset%20password%20AD%20lab.png)

### 10. Disabling a user account

Disabled the account for **John Smith** in the Finance OU — simulating an employee offboarding or a temporary access suspension.

![Account disabled - John Smith](screenshots/Disable%20user%20AD%20project.png)

### 11. Re-enabling a user account

Re-enabled **John Smith's** account — simulating a return from leave or a reversed offboarding action.

![Account enabled - John Smith](screenshots/enable%20account%20AD%20lab.png)

### 12. Active Directory Administrative Center

The AD Administrative Center provides a modern, task-based interface for managing the domain — including a built-in password reset tool and global search across all objects in `corp.local`.

![Active Directory Administrative Center](screenshots/Administrative%20Center%20Azure.png)

### 13. Creating security groups

Created department-based security groups — **IT_Admins**, **HR_Users**, **Finance_Users**, and **Sales_Users** — to manage permissions and resource access at the group level rather than per-user.

![Security groups created](screenshots/Security%20groups%20AD%20proj.png)

### 14. Managing group membership

Added **Emily Davis** as a member of the **IT_Admins** security group, demonstrating how users are assigned to groups for role-based access control.

![Group membership - IT_Admins](screenshots/Group%20membership%20Screenshot.png)

## Key takeaways

This lab covers the foundational skills behind real-world IT support and sysadmin work: every "reset my password," "I can't log in," or "set up a new hire's account" ticket a help desk agent receives is rooted in the Active Directory concepts demonstrated here — OUs, security groups, and account lifecycle management.

## Tools used

- Microsoft Azure (Free Tier)
- Windows Server 2022 Datacenter
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Active Directory Administrative Center
- Remote Desktop Protocol (RDP)
