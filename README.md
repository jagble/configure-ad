# Active Directory Lab Overview 🖥️🌐

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

## Objective 
This project is a **hands-on tutorial and walkthrough** for deploying and managing an Active Directory environment in a Windows Server ecosystem.  
It simulates real-world IT administration tasks, including creating users, joining clients to a domain, and configuring group policies.  
The lab is designed for IT professionals or students looking to gain practical experience with **Active Directory, domain management, and account security practices**.

- Deploy a Windows Server 2022 domain controller  
- Promote it to an Active Directory domain controller  
- Create and manage users and organizational units  
- Join client machines to the domain and apply group policies

## 🖋️ Languages Used
- PowerShell 🟦  

## 🏢 Environments and Technologies Used
- Windows Server 2022 (Domain Controller) 🖥️  
- Windows 10/11 (Client machines) 💻  
- Active Directory Domain Services 📂  
- Group Policy Management Console  ⚙️  
- Remote Desktop Protocol (RDP) 🖱️  
- Event Viewer 📊  
- PowerShell ISE 🔹

---

## Lab Sections

| Part | Section | Description |
|------|---------|-------------|
| 1️⃣ | [Domain Controller Setup](Domain%20Controller%20Setup.md) | Setup the Azure VM for dc-1, configure static IP, and prepare it for Active Directory. |
| 2️⃣ | [Active Directory Deployment](Active%20Directory%20Deployment.md) | Install AD DS, promote dc-1 to domain controller, and configure the initial domain. |
| 3️⃣ | [Creating Users in Powershell](Creating%20Users%20in%20Powershell.md) | Add users, configure passwords, and assign proper group memberships using PowerShell and ADUC. |
| 4️⃣ | [Group Policy & Managing Accounts](Group%20Policy%20&%20Managing%20Accounts.md) | Join client machines to the domain, verify membership, organize OUs, and apply basic group policies. |

---

> 📌 Click any section above to jump directly to that part of the lab
