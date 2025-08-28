# Group Policy & Managing Accounts

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

This section demonstrates how to manage **account lockouts, disabling/enabling accounts**, and observing logs in a domain environment using Active Directory and Group Policy.


# Configuration Steps


## Step 1: Prepare the account lockout scenario
1. Log into **DC-1**.
2. Pick a random user account created previously.
3. On **Client-1**, attempt to log in with that user **10 times using an incorrect password**.  
   - Observe that the account is not locked yet, since the default policy isn’t configured.

---

## Step 2: Configure Account Lockout Policy
1. On **DC-1**, open the **Group Policy Management Console**:

<img src="https://i.imgur.com/Guc7Bs6.png" alt="Group Policy Management" width="600"/>

2. Expand **Forest → Domains → mydomain.com**.
3. Right-click **Default Domain Policy** → **Edit**:

<img src="https://i.imgur.com/BfUrYku.png" alt="Default Domain Policy" width="600"/>

4. Navigate to:

`Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy`

5. Configure the following:

- **Account Lockout Duration:** 30 minutes  
- **Account Lockout Threshold:** 5 invalid login attempts  
- **Reset Account Lockout Counter:** 15 minutes  

<img src="https://i.imgur.com/oRQNs7Q.png" alt="Account Lockout Policy Settings" width="600"/>

6. Click **Apply** and exit the editor.

---

## Step 3: Apply Group Policy on Client-1
1. On **Client-1**, log in as `mydomain.com\jane_admin`.
2. Open **Command Prompt** and run:

```cmd
gpupdate /force
```

 <img src="https://i.imgur.com/xAq77sm.png" alt="Forcing GPUpdate" width="500"/>

## Step 4: Lock and unlock the account

Log out from Client-1 as Jane Admin.
Attempt to log in as the random user with the wrong password 7 times.
The account should now be locked.
Go back to DC-1 → ADUC, locate the random user:


  <img src="https://i.imgur.com/hYf9O1X.png" alt="Unlocking Random User" width="600"/>

Right-click → Properties, unlock the account, and apply changes.

---

## Step 5: Test the account login

Log back into Client-1 as the random user with the correct password: Password1.

  <img src="https://i.imgur.com/yVgFLVm.png" alt="Logging back in as Random User" width="600"/>

---

## Step 6: Disable and enable accounts

In ADUC, right-click the same user account → Disable Account.
Attempt login on Client-1 → login fails.
Re-enable the account → login succeeds.


---

## Step 7: Observe logs in Event Viewer

On DC-1, open Event Viewer to observe security logs related to account lockouts.

If prompted, log in as Jane Admin:

  <img src="https://i.imgur.com/FWhdqLk.png" alt="Event Viewer Login as Jane Admin" width="300"/>

Observe events:

  <img src="https://i.imgur.com/EF7ZmzJ.png" alt="Event Viewer Logs" width="500"/>


Notes:

These steps simulate real-world IT tasks, including account lockouts, unlocking accounts, disabling/enabling accounts, and monitoring logs.

This workflow demonstrates standard procedures an IT specialist would perform in a corporate Active Directory environment.
