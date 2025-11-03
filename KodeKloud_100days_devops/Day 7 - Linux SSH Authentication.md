
# Assignment

The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

**Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.**

---
# Solution

## 🧩 **Objective Summary**

We’ll set up the following connections **without requiring passwords**:

|Source (Jump Host)|Destination (App Server)|SSH Target|
|---|---|---|
|`thor@jump_host`|`stapp01.stratos.xfusioncorp.com`|`tony`|
|`thor@jump_host`|`stapp02.stratos.xfusioncorp.com`|`steve`|
|`thor@jump_host`|`stapp03.stratos.xfusioncorp.com`|`banner`|

After setup, you should be able to run:

`ssh tony@stapp01`

from the **jump host** without entering a password.

---

## 🧩 **Step 1 — Log in to the Jump Host**

Use your jump host credentials:

`ssh thor@jump_host.stratos.xfusioncorp.com`

- **User:** `thor`
- **Password:** `mjolnir123`

You’re now on the **jump host** (the central management node).

---

## 🧩 **Step 2 — Generate an SSH key pair (if not already present)**

```
ssh-keygen -t rsa -b 4096
```

### Explanation:

|Option|Meaning|
|---|---|
|**ssh-keygen**|Creates new SSH key pairs.|
|**-t rsa**|Specifies the RSA encryption algorithm.|
|**-b 4096**|Uses a strong 4096-bit key for better security.|

When prompted:

`Enter file in which to save the key (/home/thor/.ssh/id_rsa):`

→ just press **Enter** to use the default path.  
If asked about a passphrase, press **Enter** twice (leave empty) for password-less automation.

✅ Keys created:

- Private key → `/home/thor/.ssh/id_rsa`
- Public key → `/home/thor/.ssh/id_rsa.pub`

---

## 🧩 **Step 3 — Copy the public key to each App Server**

You can use `ssh-copy-id` to install your public key on each target user.

### For App Server 1

```
ssh-copy-id -i ~/.ssh/id_rsa.pub tony@stapp01.stratos.xfusioncorp.com
```

### For App Server 2

`ssh-copy-id -i ~/.ssh/id_rsa.pub steve@stapp02.stratos.xfusioncorp.com`

### For App Server 3

`ssh-copy-id -i ~/.ssh/id_rsa.pub banner@stapp03.stratos.xfusioncorp.com`

### Explanation:

|Option|Meaning|
|---|---|
|**ssh-copy-id**|Copies your local public key to the remote user’s `~/.ssh/authorized_keys`.|
|**-i ~/.ssh/id_rsa.pub**|Specifies which public key file to copy.|
|**user@host**|Destination account and hostname.|

When prompted for each server:

- Enter the respective sudo user’s password:
    
    - `tony` → `Ir0nM@n`
    - `steve` → `Am3ric@`
    - `banner` → `BigGr33n`


✅ Once done, your key will be stored in:

`/home/tony/.ssh/authorized_keys /home/steve/.ssh/authorized_keys /home/banner/.ssh/authorized_keys`

---

## 🧩 **Step 4 — Test the password-less SSH connection**

From the jump host (`thor`):

```
ssh tony@stapp01.stratos.xfusioncorp.com 
exit
```
```
ssh steve@stapp02.stratos.xfusioncorp.com 
exit 
```
```
ssh banner@stapp03.stratos.xfusioncorp.com exit
```

✅ Expected:

- No password prompt appears.
    
- You log in directly.
    
- You can exit cleanly.
    

---

## 🧩 **Step 5 — Verify file permissions (if any issues)**

If you still get password prompts, log in manually with password once and check:

`ls -ld ~/.ssh ls -l ~/.ssh/authorized_keys`

Then fix permissions:

`chmod 700 ~/.ssh chmod 600 ~/.ssh/authorized_keys`

### Explanation:

|Command|Meaning|
|---|---|
|**chmod 700 ~/.ssh**|Only the user can access `.ssh` directory.|
|**chmod 600 ~/.ssh/authorized_keys**|Only the user can read/write the key file.|

---

## 🧩 **Step 6 — Test sudo access (optional)**

From jump host, test one full chain:

`ssh tony@stapp01.stratos.xfusioncorp.com sudo -l`

You should see a list of allowed sudo commands (confirming the user is a sudoer).

---

## ✅ **Summary**

|Step|Command|Description|
|---|---|---|
|1|`ssh thor@jump_host.stratos.xfusioncorp.com`|Connect to Jump Host|
|2|`ssh-keygen -t rsa -b 4096`|Create SSH key pair|
|3|`ssh-copy-id -i ~/.ssh/id_rsa.pub user@server`|Copy key to each app server|
|4|`ssh user@server`|Verify password-less login|
|5|`chmod 700 ~/.ssh` & `chmod 600 ~/.ssh/authorized_keys`|
