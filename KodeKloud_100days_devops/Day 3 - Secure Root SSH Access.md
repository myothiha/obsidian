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


> ⚠️ Always make a backup before editing critical files:

```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

Open the SSH Configuration

```
sudo vi /etc/ssh/sshd_config
```

### Explanation:

|Part|Meaning|
|---|---|
|**sudo**|Run with administrator privileges.|
|**vi**|Text editor to open and modify the file. (You can use `nano` instead if preferred.)|
|**/etc/ssh/sshd_config**|Main configuration file for the SSH server (`sshd`).|



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

# Diagnosis and fixed if not working

## 1) Check for syntax errors first

```
sudo sshd -t -f /etc/ssh/sshd_config
```

- `sudo` — run as admin.
- `sshd` — the SSH server binary.
- `-t` — **test** the configuration (no restart; prints errors if any).
- `-f /etc/ssh/sshd_config` — **use this config file** for the test.

✅ No output = syntax OK.  
❌ If you see an error, fix that line before continuing.

---

## 2) See the **effective** value (accounts for Includes & Match)

```
sudo sshd -T | grep -i permitrootlogin
```

- `-T` — dump the **effective** configuration as the daemon sees it.
- `| grep -i permitrootlogin` — show only the `PermitRootLogin` line (case-insensitive).

If it still says `permitrootlogin yes`, there’s an override somewhere.

### (Even better) Evaluate for the **root user specifically**

`sudo sshd -T -C user=root,host=localhost,addr=127.0.0.1 | grep -i permitrootlogin`

- `-C user=… ,host=… ,addr=…` — apply **conditional** evaluation (this catches rules inside `Match` blocks).

---

## 3) Find **all** occurrences and `Match` blocks

`sudo grep -Rin --color=always -e '^[[:space:]]*PermitRootLogin' -e '^[[:space:]]*Match' /etc/ssh`

- `grep -Rin` — **R**ecursive, **i**gnore case, show **n** line numbers.
- `--color=always` — highlight matches.
- `-e '…PermitRootLogin'` — look for all definitions.
- `-e '…Match'` — show any `Match` sections that might override settings.
- `/etc/ssh` — search main config and any drop-ins.

👉 Common culprits:

- A later `PermitRootLogin yes` in the same file.
- A drop-in such as `/etc/ssh/sshd_config.d/…` setting it back to `yes`.
- A `Match User root` block overriding it.

---

## 4) Fix the conflict (choose ONE clean method)

### Method A — Edit the main file (works everywhere)

`sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak sudo vi /etc/ssh/sshd_config`

- `cp … .bak` — backup first (always a good idea).
- Open file and ensure **outside any `Match` block** you have:
    `PermitRootLogin no`
    - If you see `#PermitRootLogin yes`, **uncomment** and change to `no`.
    - **Remove or change** any later `PermitRootLogin yes`.
    - If a `Match User root` exists, change it to `no` or delete that block.


> If you previously added `PermitRootLogin no` but it’s **above** an `Include` or a `Match` that later resets it, move your line **after** those or edit the conflicting file/block.

### Method B — Use a drop-in (modern, if `Include` is present)

If your `/etc/ssh/sshd_config` contains something like:

```
Include /etc/ssh/sshd_config.d/*.conf
```

create a **last-loaded** drop-in:

```
echo 'PermitRootLogin no' | sudo tee /etc/ssh/sshd_config.d/99-disable-root-login.conf
```

- `echo … | tee file` — write text into the file as root.
- `99-…` — named so it loads **last**, overriding earlier files.

_(If `Include` isn’t supported on your distro, use Method A.)_

---

## 5) Restart the right service & check status

On RHEL/CentOS/Alma/Rocky:

```
sudo systemctl restart sshd sudo systemctl status sshd -l --no-pager
```

On Debian/Ubuntu:

```
sudo systemctl restart ssh sudo systemctl status ssh -l --no-pager
```

- `restart` — reloads the daemon with new config.
- `status` — shows whether it started cleanl
- `-l` — show full logs.
- `--no-pager` — don’t pipe to `less` (print fully).

> If restart fails, run Step 1 again to find syntax errors.

---

## 6) Re-verify the **effective** setting

```
sudo sshd -T -C user=root,host=localhost,addr=127.0.0.1 | grep -i permitrootlogin
```

Expected:

```
permitrootlogin no
```

---

## 7) Test from another terminal (keep your current session open)

`ssh root@<server>`

Expected failure:

`Permission denied (publickey,password).`

---

## 8) If it still isn’t working, check logs quickly

`sudo journalctl -u sshd -n 50 --no-pager`

- `journalctl -u sshd` — show logs for the SSH daemon.
- `-n 50` — last 50 lines.
- `--no-pager` — print all.

Look for any message that mentions `PermitRootLogin` or a drop-in being loaded later.

---

### Quick checklist (common gotchas)

- ✅ Put `PermitRootLogin no` **outside** any `Match` block.
- ✅ Ensure there’s no later `PermitRootLogin yes` in the file or drop-ins.
- ✅ Restart the correct service name (`sshd` vs `ssh`).
- ✅ Confirm with `sshd -T` (and `-C user=root`).

If you paste the output of Steps **2** and **3**, I’ll pinpoint exactly which line is overriding your setting.