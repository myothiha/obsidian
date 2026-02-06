# Assignment

The `Nautilus` system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in `Stratos DC` on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:  

a. Install `cronie` package on all `Nautilus` app servers and start `crond` service.  
b. Add a cron `*/5 * * * * echo hello > /tmp/cron_text` for `root` user.

# Solution

For each server, repeat the following step.

## ✅ **Summary**

|Step|Command|Purpose|
|---|---|---|
|1|`ssh tony@stapp01`, etc.|Connect to each app server|
|2|`sudo -i`|Become root|
|3|`yum install -y cronie`|Install cron package|
|4|`systemctl enable/start crond`|Start and enable cron daemon|
|5|`echo "*/5 * * * * echo hello > /tmp/cron_text" >> /var/spool/cron/root`|Add cron job|
|6|`crontab -l` / `cat /tmp/cron_text`|Verify setup|
|7|Repeat on all 3 servers|Ensure uniform setup|

---
## **Step 1 — Connect to each App Server**

You’ll repeat these steps for all **3 App Servers**:

```
ssh tony@stapp01        # App Server 1 
ssh steve@stapp02       # App Server 2 
ssh banner@stapp03      # App Server 3
```

|Server|User|Password|
|---|---|---|
|stapp01|tony|Ir0nM@n|
|stapp02|steve|Am3ric@|
|stapp03|banner|BigGr33n|

---

## 🧩 **Step 2 — Switch to root user**

`sudo -i`

|Part|Meaning|
|---|---|
|**sudo -i**|Opens an interactive root shell so you can run admin commands.|

You’ll see the prompt change to `root@stapp0X`.

---

## 🧩 **Step 3 — Install the `cronie` package**

```
yum install -y cronie
```

|Option|Meaning|
|---|---|
|**yum**|Package manager for RHEL/CentOS systems.|
|**install**|Installs the specified package.|
|**-y**|Automatically answers “yes” to any prompts.|
|**cronie**|Package providing the cron daemon (`crond`) used to schedule recurring jobs.|

✅ Expected output (snippet):

`Installed:   cronie.x86_64 0:1.5.2-4.el7`

---

## 🧩 **Step 4 — Start and enable the cron daemon**

```
systemctl enable crond 
systemctl start crond
```

|Command|Meaning|
|---|---|
|**systemctl enable crond**|Enables `crond` to **start automatically on boot**.|
|**systemctl start crond**|Starts the cron service **immediately**.|

✅ Check status (optional):

`systemctl status crond`

You should see:

`Active: active (running)`

---

## 🧩 **Step 5 — Add the cron job for root**

We’ll add the line directly to root’s crontab.

```
echo "*/5 * * * * echo hello > /tmp/cron_text" >> /var/spool/cron/root
```

### Explanation

|Part|Meaning|
|---|---|
|**echo**|Prints the given text.|
|**"*/5 * * * * echo hello > /tmp/cron_text"**|The actual cron job entry.|
|**>> /var/spool/cron/root**|Appends it to the **root user’s crontab file**.|

> 💡 You can also edit manually using:
> 
> `crontab -e`
> 
> and then add:
> 
> `*/5 * * * * echo hello > /tmp/cron_text`
> 
> Save and exit (Ctrl+O, Enter, Ctrl+X in nano).

---

### Cron schedule breakdown

|Field|Meaning|Example|
|---|---|---|
|`*/5`|Every 5 minutes|runs every 5 min|
|`*`|Every hour|applies all hours|
|`*`|Every day|applies all days|
|`*`|Every month|applies all months|
|`*`|Every weekday|applies all weekdays|

So this command runs **every 5 minutes**, writing “hello” to `/tmp/cron_text`.

---

## 🧩 **Step 6 — Verify the cron job**

List root’s crontab:

```
crontab -l
```

✅ Expected output: `*/5 * * * * echo hello > /tmp/cron_text`

Then wait 5–10 minutes and confirm that the cron ran:

```
cat /tmp/cron_text
```

✅ Expected: `hello`

---

## 🧩 **Step 7 — Repeat for all app servers**

Perform the same steps (2–6) on:

- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

---
