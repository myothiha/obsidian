# Assignment

In a bid to automate backup processes, the `xFusionCorp Industries` sysadmin team has developed a new bash script named `xfusioncorp.sh`. While the script has been distributed to all necessary servers, it lacks executable permissions on `App Server 2` within the Stratos Datacenter.  

Your task is to grant executable permissions to the `/tmp/xfusioncorp.sh` script on `App Server 2`. Additionally, ensure that all users have the capability to execute it.

# Main concept: all users must have both read and execute permission. (not just execution)
## 🧩 **Step 1 — Connect to App Server 2**

`ssh steve@stapp02`

|Part|Meaning|
|---|---|
|**ssh**|Secure Shell, used to log in remotely.|
|**tony@stapp02**|Log in as user `tony` on App Server 2.|

---

## 🧩 **Step 2 — Verify the script exists**

`ls -l /tmp/xfusioncorp.sh`

|Option|Meaning|
|---|---|
|**-l**|“Long” listing format — shows owner, group, permissions, and file details.|

✅ Example output (before fixing):

`-rw-r--r-- 1 root root 1234 Oct 24 22:10 /tmp/xfusioncorp.sh`

Here the `x` (execute) bit is **missing** for everyone.

---

## 🧩 **Step 3 — Grant execute permission to all users**

`sudo chmod a+x /tmp/xfusioncorp.sh`

|Part|Meaning|
|---|---|
|**sudo**|Run as administrator — needed because the file is likely owned by root.|
|**chmod**|“Change mode” — modifies file permissions.|
|**a+x**|Add execute (`x`) permission for **all**:  <br>• `u` = user (owner)  <br>• `g` = group  <br>• `o` = others  <br>`a` means “all of them.”|
|**/tmp/xfusioncorp.sh**|Path to the file.|

After this, **everyone can execute** the script.

---

## 🧩 **Step 4 — Confirm permissions changed**

`ls -l /tmp/xfusioncorp.sh`

✅ Expected output:

`-rwxr-xr-x 1 root root 1234 Oct 24 22:10 /tmp/xfusioncorp.sh`

Now there’s an `x` in each permission group:

- `rwx` → owner can read/write/execute
- `r-x` → group can read/execute
- `r-x` → others can read/execute

---

## 🧩 **Step 5 — Test execution**

Try running the script:

`/tmp/xfusioncorp.sh`

If it prints output (or even an error from inside the script), the permission part is working.

If it says _“Permission denied”_ still, double-check:

`ls -ld /tmp`

to ensure `/tmp` itself has the `x` (execute / traverse) bit — it should (`drwxrwxrwt`).

---

## ✅ **Summary**

| Step | Command                              | Purpose                        |
| ---- | ------------------------------------ | ------------------------------ |
| 1    | `ssh tony@stapp02`                   | Connect to App Server 2        |
| 2    | `ls -l /tmp/xfusioncorp.sh`          | Verify file                    |
| 3    | `sudo chmod a+x /tmp/xfusioncorp.sh` | Add execute permission for all |
| 4    | `ls -l /tmp/xfusioncorp.sh`          | Confirm permission change      |
| 5    | `/tmp/xfusioncorp.sh`                | Test execution                 |