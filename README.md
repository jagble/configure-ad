# Active Directory Configuration

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

# Configuration Steps


## Step 1: Create a Resource Group in Azure 🌐

1. **Navigate to the Azure Portal** and select **Resource Groups** from the left menu. 🖥️
2. Click **+ Create** to start a new resource group. ➕
3. **Fill in the Details**:
   - **Subscription**: Choose your subscription. 📑
   - **Resource Group Name**: Enter a unique name (e.g., `LabRG`). 🏷️
   - **Region**: Select the region where you want to deploy your resources (e.g., **East US**). 🌍
4. Ensure **Validation Passed** appears, then click **Create** to deploy the resource group. ✅

   <img src="https://i.imgur.com/KQYpfMo.png" alt="Azure Resource Group Creation" width="400"/>

---

## Step 2: Create a Virtual Network (VNet) 🌐

1. **Navigate to the Azure Portal** and select **Virtual Networks** from the left menu. 🌍
2. Click **+ Add** to create a new VNet. ➕
3. **Fill in the VNet Details**:
   - **Subscription**: Choose your subscription. 📑
   - **Resource Group**: Select the resource group you created in Step 1. 🏷️
   - **VNet Name**: Enter a unique name for the VNet (e.g., `LabVNet`). 🌐
   - **Region**: Choose the same region as your resource group (e.g., **East US**). 🌎
4. Under **IP Addresses**, configure the address space and subnets. 🌐
5. Click **Review + Create** and then **Create** to deploy the VNet. ✅

   <img src="https://i.imgur.com/GNNSLXz.png" alt="Azure VNet Creation" width="500"/>

---

## Step 3: Create the Domain Controller VM (dc-1) 🖥️

1. **Navigate to the Azure Portal** and select **Virtual Machines** from the left menu. 🖥️
2. Click **+ Add** to create a new VM. ➕
3. **Fill in the VM Details**:
   - **Subscription**: Choose your subscription. 📑
   - **Resource Group**: Select the resource group you created earlier. 🏷️
   - **VM Name**: Name the VM `dc-1` (Domain Controller). 🏢
   - **Region**: Choose the same region as your VNet. 🌎
   - **Image**: Select **Windows Server 2022**. 💻
   - **Size**: Choose an appropriate size (e.g., Standard B1s). ⚙️
   - **Authentication**: Choose a username and password or SSH key for access. 🔑

   <img src="https://i.imgur.com/AljwqKt.png" alt="VM Configuration" width="400"/>
   <img src="https://i.imgur.com/noHmq5S.png" alt="VM Networking" width="400"/>

4. **Networking Configuration**:
   - In the **Networking** tab, make sure the **Virtual Network** is set to the VNet you created earlier (e.g., `LabVNet`).
   - Choose the **Subnet** where you want the VM to reside (usually the default one). 🌐


5. Once everything is configured, click **Review + Create** and then **Create** to deploy the VM. ✅

---

   ## Step 4: Set Static IP and Disable Firewall 🔒

1. **Go to the Networking Tab** for the `dc-1` VM after creation. 🌐
2. **Set the Private IP to Static**:
   - In the **Networking** section, ensure that the **Private IP** is set to **Static**. This ensures that the IP address doesn’t change after reboots.
   
   <img src="https://i.imgur.com/AGyRMSq.png" alt="Static IP Configuration" width="500"/>

3. **Disable the Firewall**:
   - Open **Windows Defender Firewall with Advanced Security** on `dc-1`.
   - In the left pane, select **Windows Defender Firewall with Advanced Security**.
   - For each of the **Domain**, **Private**, and **Public** profiles, turn off the firewall by selecting **Turn off Windows Defender Firewall**.
 
 <img src="https://i.imgur.com/opqOoFj.png" alt="Static IP Configuration" width="500"/>
4. Once these changes are made, the VM should be ready for the next configuration steps.

---

## Step 5: Set Up the Client VM (client-1) 💻

1. **Navigate to the Azure Portal** and select **Virtual Machines** from the left menu. 🖥️
2. Click **+ Add** to create a new VM. ➕
3. **Fill in the VM Details**:
   - **Resource Group**: Select the same resource group as `dc-1`. 🏷️
   - **VM Name**: Name the VM `client-1` (Client Machine). 🏢
   - **Region**: Choose the same region as `dc-1` and the VNet. 🌎
   - **Image**: Select **Windows 10**. 💻
   - **Size**: Choose a size with at least **2 vCPUs** (e.g., **Standard B2s**). ⚙️
   - **Authentication**: Choose a username and password for access. 🔑

4. **Networking Configuration**:
   - In the **Networking** tab, ensure that the **Virtual Network** is set to the same **VNet** you created earlier (e.g., `LabVNet`).
   - Choose the same **Subnet** as `dc-1`.

5. Once everything is configured, click **Review + Create** and then **Create** to deploy the `client-1` VM. ✅

---

## Step 6: Set Client-1's DNS Settings to dc-1's Private IP in Azure 🔧

1. **Find dc-1's Private IP in Azure**:
   - In the **Azure Portal**, go to **Virtual Machines** and select `dc-1`.
   - Under **Networking**, find the **Private IP address** assigned to `dc-1`. Copy this IP.

2. **Navigate to Client-1's Network Interface**:
   - In the **Azure Portal**, go to **Virtual Machines** and select `client-1`.
   - Under the **Settings** section, select **Networking**.
   - In the **Network Interface** section, click on the **NIC card**.
  
  <img src="https://i.imgur.com/j8ADzIf.png" alt="Static IP Configuration" width="400"/>

3. **Modify DNS Settings for Client-1**:
   - In the **DNS servers** section, select **Custom**.
   - Enter `dc-1`'s **Private IP address** that you copied earlier.
   - Click **Save** to apply the changes.
  
  <img src="https://i.imgur.com/Q1AlyTp.png" alt="Static IP Configuration" width="400"/>

4. **Verify DNS Settings**:
   - Once saved, Client-1’s DNS settings will be configured to use `dc-1`'s private IP address.

---

## Step 7: Test Connectivity and Verify DNS Settings 🖧

1. **Log into Client-1**:
   - Use **RDP** to log into the `client-1` VM. 🔑

2. **Ping dc-1's Private IP**:
   - Open **Command Prompt** or **PowerShell** on `client-1`.
   - Run the following command to ping `dc-1`'s private IP:
   ```powershell
   ping <dc-1_Private_IP>

 <img src="https://i.imgur.com/Tu235H4.png" alt="Static IP Configuration" width="400"/>

  - Ensure the ping is successful. You should see reply messages indicating that client-1 can reach dc-1.

3. Verify DNS Settings:

    - Open PowerShell and run the following command: `ipconfig /all`
    - Look for the DNS Servers section in the output. It should show dc-1's private IP address as the DNS server.
  
  <img src="https://i.imgur.com/ItFlStL.png" alt="Static IP Configuration" width="500"/>
