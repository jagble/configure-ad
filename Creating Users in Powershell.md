# Creating New Users in Powershell

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

# Configuration Steps
## Step 1: Log into Client-1 as Domain Admin** 🔑

- Open **RDP** and log into **Client-1**.
- Use the domain admin credentials:
  - **Username:** `mydomain.com\jane_admin`
  - **Password:** `Password123`
- Ensure you are connected to the domain.

## Step 2: Prepare PowerShell Script to Create Users 🖥️

1. On `client-1`, **open PowerShell ISE as Administrator**.  
2. Click **File → New** to create a new script file.  
3. **Save the file to the Desktop** with a name like `createusers.ps1`.  
4. Copy and paste the script into the file. You can access it directly here: [Generate Names Script](.\docs/Generate-Names-Create-Users.ps1)  
5. Save the file after pasting the script.
