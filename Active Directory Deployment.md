# Active Directory Deployment

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

# Configuration Steps

## Step 1: Log into dc-1 and Open Server Manager 🖥️

1. Make sure you are **logged into the dc-1 VM** using RDP.  
2. Once logged in, click the **Start Menu** and search for **Server Manager**.  
3. Click to open **Server Manager**, which is the central hub for managing roles, features, and server settings on Windows Server 2022.  

   <img src="https://i.imgur.com/WzXFBFh.png" alt="Open Server Manager" width="500"/>

> **Note:** Server Manager is where you'll install Active Directory and other roles for the server.



## Step 2: Add Active Directory Domain Services Role 🏗️

1. In **Server Manager**, click on **Add roles and features**.  
2. In the wizard, click **Next** until you reach **Select server roles**.  
3. Check **Active Directory Domain Services (AD DS)**.  
4. When the pop-up appears, click **Add Features** to include the required supporting features.  
5. Continue clicking **Next** until you reach **Confirm installation selections**.  
6. Check the box **Restart the destination server automatically if required**.  
7. Click **Install** and wait for the installation to complete.  

   <img src="https://i.imgur.com/NhyLFRJ.png" alt="Add AD DS Role" width="600"/>


## Step 3: Promote dc-1 to a Domain Controller 🌐

1. After AD DS installation completes, click the **notification flag** in the top-right of Server Manager.  
   
   <img src="https://i.imgur.com/UMe7wBF.png" alt="Notification Flag" width="600"/>

2. Click **Promote this server to a domain controller**.  
3. In the wizard:  
   - **Deployment Configuration**: Select **Add a new forest**  

   <img src="https://i.imgur.com/yl7Unbz.png" alt="Add New Forest" width="600"/>

   - **Root domain name**: `mydomain.com`  
4. Set the **Directory Services Restore Mode (DSRM) password**.  
   - For this lab, we can use `Password1` since we won’t use it.  
5. **Uncheck** the box that says **Create DNS delegation**.  

   <img src="https://i.imgur.com/EhiXFzZ.png" alt="Uncheck DNS Delegation" width="600"/>

6. Continue through the wizard and review your selections.  
7. Click **Install**. The server will automatically restart after promotion.


------------------

## Step 4: Create Organizational Units (OUs) 🏢

1. After the server restarts from the domain controller promotion, log into **dc-1**.  
2. Open **Active Directory Users and Computers (ADUC)** from the Start menu.  

   <img src="https://i.imgur.com/fXDmyn9.png" alt="Finding ADUC in Start Menu" width="600"/>

3. ADUC will open and show the domain structure.  

   <img src="https://i.imgur.com/eKWTvEL.png" alt="ADUC Open" width="600"/>

4. Create two **Organizational Units (OUs)**:  
   - `_EMPLOYEES`  
   - `_ADMINS`  

   <img src="https://i.imgur.com/wioRlag.png" alt="Adding OUs" width="600"/>

5. Once both OUs are created, they should look like this:  

   <img src="https://i.imgur.com/opRevsT.png" alt="Completed OUs" width="600"/>

> **Note:** OUs help organize users and groups in the domain. The `_ADMINS` OU will be used to store administrative accounts, while `_EMPLOYEES` can store regular domain users.

---

## Step 5: Create Domain Admin User 👤

1. Inside the `_ADMINS` OU, click on **New User**.  

   <img src="https://i.imgur.com/DTx3tXa.png" alt="Adding New User in Admin OU" width="600"/>

2. Fill out the user information for **Jane Doe**:  

   <img src="https://i.imgur.com/wyhYy19.png" alt="Filling Out Jane Doe Info" width="400"/>

3. Set the password to `Password123` and configure the password settings:  
   - Uncheck **“User must change password at next logon”**  
   - Check **“Password never expires”**  

   <img src="https://i.imgur.com/93LzelZ.png" alt="Password Settings for Jane Doe" width="400"/>

4. Once done, the user creation is complete and should look like this:  

   <img src="https://i.imgur.com/mM0J6hZ.png" alt="Jane Doe Created in ADUC" width="600"/>

5. **Add Jane Doe to the built-in Domain Admins group**:  
   - Right-click on `Jane Doe` → **Properties** → **Member Of** → **Add**  
   - Type `Domain Admins`, click **Check Names**, then click **Apply**  

   <img src="https://i.imgur.com/Blknm0u.png" alt="Adding Jane to Domain Admins Group" width="400"/>

6. **Log out of dc-1** and log back in as the new domain admin account:  

   ```text
   Username: mydomain.com\jane_admin
   Password: Password123

  <img src="https://i.imgur.com/4EyIX81.png" alt="Logging in as Jane Doe" width="400"/>



## Step 6: Join Client VM to the Domain 🌐💻

1. **Keep `dc-1` open** while logged in as Jane Doe. Open a **new RDP session** and log into `client-1`.

2. On `client-1`, **right-click the Start Menu** and go to **System**.

3. Scroll down and click **Advanced system settings**.

4. In the pop-up window, click on **Computer Name** → **Change**:  

   <img src="https://i.imgur.com/YxYGqoX.png" alt="Computer Name Change" width="400"/>

5. Select **Domain**, type `mydomain.com`, and click **OK**.

6. When prompted, log in using the **domain admin account**:  

   ```text
   Username: mydomain.com\jane_admin
   Password: Password123

**Verify** in `dc-1` that `client-1` is now a member of the domain:
   - Open **Active Directory Users and Computers**
   - Look under the **Computers** folder and ensure `client-1` is listed.

## Step 7. Create OU for Clients 📂

1. In **Active Directory Users and Computers**, right-click your domain → **New** → **Organizational Unit**.

2. Name the OU: `_CLIENTS`

3. Drag `client-1` from the **Computers** folder into the `_CLIENTS` OU.
