“There are times to stay put, and what you want will come to you, and there are times to go out into the world and find such a thing for yourself.”
# Assignment

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

# Solution

## 🧩 **Step 1 — Connect to each App Server**

Repeat the following steps on **every App Server** (for example, App Server 1, 2, and 3).

```
ssh tony@stapp01
```

Then later:

```
ssh tony@stapp02
ssh tony@stapp03
```

### Explanation:

|Part|Meaning|
|---|---|
|**ssh**|Secure Shell — connects securely to another Linux machine.|
|**tony@stapp01**|Login as user `tony` on server `stapp01` (App Server 1).|

---

## 🧩 **Step 2 — Open the SSH configuration file**

```
sudo vi /etc/ssh/sshd_config
```

### Explanation:

|Part|Meaning|
|---|---|
|**sudo**|Run with administrator privileges.|
|**vi**|Text editor to open and modify the file. (You can use `nano` instead if preferred.)|
|**/etc/ssh/sshd_config**|Main configuration file for the SSH server (`sshd`).|

> ⚠️ Always make a backup before editing critical files:
> 
> `sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak`

---

## 🧩 **Step 3 — Locate the root login directive**

Inside the file, find the line:

`#PermitRootLogin yes`

It might be commented (with `#`) or set to `yes`.

---

## 🧩 **Step 4 — Modify it to disable root login**

Change that line to:

`PermitRootLogin no`

### Explanation:

|Option|Meaning|
|---|---|
|**PermitRootLogin**|Controls whether root can log in directly via SSH.|
|**no**|Completely disables SSH access for root.|

> ✅ Remove the `#` at the beginning if present (uncomment it).

---

## 🧩 **Step 5 — Save and exit the editor**

If using **vi**:

- Press `Esc`
    
- Type `:wq`
    
- Press `Enter`
    

If using **nano**:

- Press `Ctrl + O` → `Enter` → `Ctrl + X`
    

---

## 🧩 **Step 6 — Restart the SSH service**

`sudo systemctl restart sshd`

### Explanation:

|Part|Meaning|
|---|---|
|**systemctl**|Command to control (start/stop/restart) system services.|
|**restart**|Restarts the specified service.|
|**sshd**|The SSH daemon (server process).|

✅ This applies your configuration change immediately.

---

## 🧩 **Step 7 — Verify SSH root login is disabled**

You can test it from any machine:

`ssh root@stapp01`

Expected result:

`Permission denied (publickey,password).`

or

`Access denied.`

That confirms direct SSH login for root is **disabled**.

---

## 🧩 **Step 8 — (Repeat for All Servers)**

Perform **Steps 1 through 7** on **all app servers** (`stapp01`, `stapp02`, `stapp03`).

---

## ✅ **Summary**

| Step | Command                                                 | Description                  |
| ---- | ------------------------------------------------------- | ---------------------------- |
| 1    | `ssh tony@stapp0X`                                      | Connect to each App Server   |
| 2    | `sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak` | Backup SSH config            |
| 3    | `sudo vi /etc/ssh/sshd_config`                          | Edit SSH configuration       |
| 4    | `PermitRootLogin no`                                    | Disable root login           |
| 5    | `sudo systemctl restart sshd`                           | Apply changes                |
| 6    | `ssh root@stapp0X`                                      | Verify root login is blocked |