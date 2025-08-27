# Active Directory Lab Overview

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

## Objective 
The objective of this lab is to demonstrate the process of deploying an Active Directory environment, creating and managing users, setting up a domain controller, and applying group policies. This lab will guide you through configuring a basic Active Directory environment in Azure and on client machines.

---

## Lab Sections

1. [Domain Controller Setup](Domain%20Controller%20Setup.md)  
   Setup the Azure infrastructure, deploy the Windows Server 2022 VM (dc-1), configure static IP, and prepare it for Active Directory.

2. [Active Directory Deployment](Active%20Directory%20Deployment.md)  
   Promote dc-1 to a domain controller, install AD DS, create OUs, and configure initial domain settings.

3. [Creating Users in Powershell](Creating%20Users%20in%20Powershell.md)  
   Add domain users, configure passwords, and assign proper group memberships using PowerShell and ADUC.

4. [Group Policy & Managing Accounts](Group%20Policy%20&%20Managing%20Accounts.md)  
   Join client machines to the domain, verify domain membership, organize users and computers into OUs, and apply basic group policies.

---

> 📌 Click each part to jump directly to the respective section of the lab.
