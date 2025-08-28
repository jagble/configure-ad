# Group Policy & Managing Accounts

<p align="center">
  <img src="https://i.imgur.com/gUKUoFk.png" alt="Azure Setup" width="500"/>
</p>

This section demonstrates how to manage **account lockouts, disabling/enabling accounts**, and observing logs in a domain environment using Active Directory and Group Policy.


# Configuration Steps

This section demonstrates how to manage **account lockouts, disabling/enabling accounts**, and observing logs in a domain environment using Active Directory and Group Policy.

---

## Step 1: Log in and simulate a lockout
1. Log into **DC-1** as `mydomain.com\jane_admin`.
2. Pick a **random user** created previously in the `_EMPLOYEES` OU.
3. Attempt to log into **Client-1** **10 times** with a **wrong password**.
4. Observe that the account is **not actually locked yet** in Active Directory.

---

## Step 2: Open Group Policy Management
1. On **DC-1**, click **Start** and type:

   ```text
   gpmc.msc

2. Open Group Policy Management Console

  Figure 1: Group Policy Management Console

3. Expand the tree:

  - Forest → mydomain.com → Domains → mydomain.com

4. Find Default Domain Policy:

   Figure 2: Locating Default Domain Policy

5. Right-click Default Domain Policy and select Edit.


## Step 3: Configure Account Lockout Policy

Navigate to:

Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy


Modify the following settings:


Figure 3: Account Lockout Policy settings

Account lockout duration: 30 minutes

Account lockout threshold: 5 invalid attempts

Reset account lockout counter: 15 minutes

Press Apply and exit the editor.


## Step 4: Force Group Policy Update on Client

Log into Client-1 as mydomain.com\jane_admin.

Open Command Prompt as administrator.

Run the following command:

gpupdate /force



Figure 4: Forcing Group Policy update on Client-1

Wait for the confirmation that the policy has been updated.


## Step 5: Test Lockout

Log out of Jane Admin on Client-1.

Log in with the random user and attempt 7 invalid login attempts.

The account should now display a locked account message.

On DC-1, open Active Directory Users and Computers:

Navigate to the random user account.

Right-click → Properties.

Check Unlock account and click Apply.


Figure 5: Unlocking the user account in Active Directory

Return to Client-1 and log in with the unlocked account:


Figure 6: Logging in as the unlocked user

## Step 6: Disable and Enable Accounts

On DC-1, pick a random user.

Right-click → Properties → uncheck Account is enabled.

Attempt to log in on Client-1 with that account:

You should see a login failure.

Re-enable the account and test logging in again.


## Step 7: Observing Logs

Open Event Viewer on DC-1 and Client-1.


Figure 7: Event Viewer showing logs

When prompted for administrator privileges, log in as Jane Admin:


Figure 8: Logging in as Jane Admin for Event Viewer

Observe the Security Logs for:

Account lockouts

Failed login attempts

Successful logins
