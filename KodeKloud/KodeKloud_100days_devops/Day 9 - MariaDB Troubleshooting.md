
# Assignment

There is a critical issue going on with the `Nautilus` application in `Stratos DC`. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.  

Look into the issue and fix the same.

---
# Solution


## Summary

Error: Data directory `/var/lib/mysql` is missing.

Solution:

```
mkdir /var/lib/mysql
chown -R mysql:mysql /var/lib/mysql
chmod 750 /var/lib/mysql
systemctl restart mariadb
```


## 🧩 **Objective Summary**

**Goal:**  
Fix the issue so that the **MariaDB service** runs properly on the **database server**.

**Server details (from your infrastructure list):**

|Server|IP|User|Password|Purpose|
|---|---|---|---|---|
|stdb01|172.16.239.10|peter|Sp!dy|Nautilus Database Server|

---

## 🧩 **Step 1 — Connect to the Database Server**

From your **jump host** (or local terminal if connected through VPN):

```
ssh peter@stdb01
```

Then enter the password:

`Sp!dy`

---

## 🧩 **Step 2 — Check the MariaDB service status**

```
sudo systemctl status mariadb
```

### Explanation

|Part|Meaning|
|---|---|
|**sudo**|Run as admin (root privileges).|
|**systemctl status mariadb**|Shows if the MariaDB service is active, failed, or inactive.|

You might see something like:

`● mariadb.service - MariaDB 10.x database server    Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled)    Active: failed (Result: exit-code)`

---

## 🧩 **Step 3 — Attempt to start the service**

```
sudo systemctl start mariadb
```

Then recheck the status:

`sudo systemctl status mariadb`

✅ If it says:

`Active: active (running)`

🎉 Great — the issue is fixed!

If it still fails, proceed to diagnostics below.

---

## 🧩 **Step 4 — Check the error log**

MariaDB usually writes logs to: `/var/log/mariadb/mariadb.log`

or sometimes: `/var/log/mysql/mysqld.log`

Check recent messages:

```
sudo tail -20 /var/log/mariadb/mariadb.log
```

Also use

```
sudo systemctl status mariadb -l --no-pager
```
### Common errors you might see:

|Error message|Meaning|Fix|
|---|---|---|
|`Can't start server: Bind on TCP/IP port: Address already in use`|Port 3306 is already used by another process.|Kill the conflicting process or free port 3306.|
|`Permission denied`|Data directory or log file has wrong ownership.|Fix ownership: `sudo chown -R mysql:mysql /var/lib/mysql`|
|`InnoDB: Unable to lock ./ibdata1`|Old MariaDB process didn’t shut down cleanly.|Remove PID file: `sudo rm -f /var/run/mariadb/mariadb.pid`|

---
### Error Found

`mariadb-prepare-db-dir[2404]: Make sure the /var/lib/mysql is empty before running mariadb-prepare-db-dir.`

### Solution:

#### 0) Connect and get root

`ssh peter@stdb01 sudo -i`

- `ssh peter@stdb01` — log into the DB server.
- `sudo -i` — start a root login shell (we’ll need root for service and datadir work).

---

#### 1) Quick checks: what’s in the datadir?

`ls -la /var/lib/mysql test -d /var/lib/mysql/mysql && echo "system tables present" || echo "system tables missing"`

- `ls -la` — long listing incl. hidden files (to see what’s there).
- `test -d /var/lib/mysql/mysql` — checks if the **mysql system database directory** exists.
    - `&& echo ... || echo ...` — prints which case you’re in.
        

If system tables are **present**, the issue is likely ownership/permissions.  
If **missing**, we need to initialize the datadir.

#### In this assignment, the data dir is missing so, create it and assign appropriate owner.

```
mkdir /var/lib/mysql
chown -R mysql:mysql /var/lib/mysql
chmod 750 /var/lib/mysql
systemctl restart mariadb
```

#### Check again

```
systemctl status mariadb
```

Expected Output: `Active (running)`

---

## 🧩 **Step 5 — Fix common problems**

### 🛠️ Case 1: PID file leftover

`sudo rm -f /var/run/mariadb/mariadb.pid sudo systemctl start mariadb`

### 🛠️ Case 2: Incorrect data directory ownership

`sudo chown -R mysql:mysql /var/lib/mysql sudo systemctl restart mariadb`

### 🛠️ Case 3: Port 3306 conflict

Find the process:

`sudo lsof -i :3306`

If something else is using it:

`sudo kill -9 <PID> sudo systemctl start mariadb`

---

## 🧩 **Step 6 — Enable MariaDB to start on boot**

Once fixed, make it permanent:

`sudo systemctl enable mariadb`

|Option|Meaning|
|---|---|
|**enable**|Ensures service auto-starts at boot.|

---

## 🧩 **Step 7 — Verify it’s working**

Check:

`sudo systemctl status mariadb`

✅ Should show:

`Active: active (running)`

Then test connection:

`mysql -u root -p`

Press Enter (if no root password set) or use the configured password.

---

## 🧩 **Step 8 — Confirm application connectivity**

If your Nautilus app connects via localhost or the DB server’s IP (172.16.239.10),  
the database should now accept connections on port **3306** again.

You can verify:

`sudo netstat -tulnp | grep 3306`

✅ Expected:

`tcp   0   0 0.0.0.0:3306   0.0.0.0:*   LISTEN   1234/mysqld`

---

## ✅ **Summary**

|Step|Command|Purpose|
|---|---|---|
|1|`ssh peter@stdb01`|Connect to DB server|
|2|`sudo systemctl status mariadb`|Check MariaDB service|
|3|`sudo systemctl start mariadb`|Try to start service|
|4|`sudo tail -20 /var/log/mariadb/mariadb.log`|Check for errors|
|5|Fix PID / ownership / port|Resolve common issues|
|6|`sudo systemctl enable mariadb`|Start MariaDB on boot|
|7|`mysql -u root -p`|Verify DB access|
|8|`netstat -tulnp|grep 3306`|