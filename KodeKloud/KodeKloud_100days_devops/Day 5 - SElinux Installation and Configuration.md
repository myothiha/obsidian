# Assignment

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for `App server 2` in the `Stratos Datacenter:`  

1. Install the required `SELinux` packages.
2. Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
3. No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
4. Disregard the current status of SELinux via the command line; the final status after the reboot should be `disabled`.

# Solution

---
### 🧠 Quick Recap

1️⃣ Connect to App Server 2 → `ssh steve@stapp02`  
2️⃣ Become root → `sudo -i`  
3️⃣ Install packages → `yum install -y selinux-policy selinux-policy-targeted`  
4️⃣ Edit `/etc/selinux/config` → set `SELINUX=disabled`  
5️⃣ Save changes → reboot not needed now  
6️⃣ Verify configuration → `grep SELINUX= /etc/selinux/config`

---
## 🧩 **Step 1 — Connect to App Server 2**

```
ssh steve@stapp02
```

|Part|Meaning|
|---|---|
|**ssh**|Secure Shell — connects securely to another Linux system.|
|**steve@stapp02**|Connect to App Server 2 using user `steve` (as per stored credentials).|

> Password: `Am3ric@`

---

## 🧩 **Step 2 — Switch to root or sudo**

You’ll need administrative rights to manage SELinux: 

```
sudo -i
```

|Part|Meaning|
|---|---|
|**sudo -i**|Starts an interactive root shell, letting you run root commands directly.|

---

## 🧩 **Step 3 — Install SELinux packages**

On **CentOS/RHEL systems** (which Stratos servers typically use):

```
yum install -y selinux-policy selinux-policy-targeted
```

### Explanation

|Option|Meaning|
|---|---|
|**yum**|The package manager for RHEL/CentOS.|
|**install**|Installs specified packages.|
|**-y**|Automatically answer “yes” to all prompts.|
|**selinux-policy**|The base SELinux policy framework.|
|**selinux-policy-targeted**|Default policy that applies SELinux restrictions to specific services/processes.|

✅ This ensures SELinux is installed and ready for configuration.

---

## 🧩 **Step 4 — Check the current SELinux status**

```
sestatus
```

|Command|Meaning|
|---|---|
|**sestatus**|Displays SELinux status (enabled, enforcing, permissive, disabled).|

You might see:

`SELinux status:                 enabled Current mode:                   enforcing`

⚠️ **We will disable it permanently**, so ignore the current state for now.

---

## 🧩 **Step 5 — Permanently disable SELinux**

Open the main configuration file:

```
sudo vi /etc/selinux/config
```

|Part|Meaning|
|---|---|
|**vi**|Text editor to modify files.|
|**/etc/selinux/config**|Main SELinux configuration file — determines mode at boot.|

---

### Inside the file, look for:

`SELINUX=enforcing`

Change it to:

`SELINUX=disabled`

Then save and exit:

- Press `Esc`
- Type `:wq`
- Press `Enter`

---

### ✅ Explanation of SELINUX modes

|Mode|Description|
|---|---|
|**enforcing**|SELinux fully enforces policies (active protection).|
|**permissive**|Logs policy violations but doesn’t block actions.|
|**disabled**|SELinux is completely off (inactive).|

We’re setting it to **disabled** for now, per the instructions.

---

## 🧩 **Step 6 — Verify the change in the configuration file**

Check the file content:

```
grep SELINUX= /etc/selinux/config
```

✅ Expected output:

`SELINUX=disabled`

That confirms it’s **permanently disabled**, effective after the next reboot.

---

## 🧩 **Step 7 — Confirm no reboot is needed now**

You don’t need to reboot — the question says maintenance reboot is already scheduled.  
However, you can verify that after reboot, SELinux **will be disabled**:

```
cat /etc/selinux/config | grep SELINUX=
```

Output should show:

`SELINUX=disabled`

That’s sufficient for now.

---

## ✅ **Final Verification Summary**

|Check|Command|Expected Output|
|---|---|---|
|Packages installed|`rpm -qa|grep selinux`|
|Config file setting|`grep SELINUX= /etc/selinux/config`|`SELINUX=disabled`|
|Runtime status|`sestatus`|Ignore current state (it will disable after reboot)|

---
