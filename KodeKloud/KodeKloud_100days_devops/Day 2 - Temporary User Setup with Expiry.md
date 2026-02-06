# Task

As part of the temporary assignment to the `Nautilus` project, a developer named `javed` requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:  

Create a user named `javed` on `App Server 2` in Stratos Datacenter. Set the expiry date to `2024-04-15`, ensuring the user is created in lowercase as per standard protocol.

> Note: You can find the infrastructure details by clicking on the **Details of all Users and Servers** button on the top-right section of the page.

# Solution

## ✅ **Summary**

| Step | Command                               | Purpose                      |
| ---- | ------------------------------------- | ---------------------------- |
| 1    | `ssh tony@stapp02`                    | Connect to App Server 2      |
| 2    | `sudo useradd -m -e 2024-04-15 javed` | Create user with expiry date |
| 3    | `sudo passwd javed`                   | Set user password            |
| 4    | `sudo chage -l javed`                 | Verify expiry date           |
| 5    | _(optional)_ `grep javed /etc/shadow` | Confirm expiry value         |
| 6    | _(optional)_ `su - javed`             | Test login before expiry     |
## 🧩 **Step 1 – Log in to App Server 2**

If your environment has multiple servers, make sure you’re inside **App Server 2**.  
You can usually connect using:

`ssh tony@stapp02`

_(replace `tony` with your admin username if different)_

- **ssh** — Secure Shell, used to log in remotely.
- **@stapp02** — The server’s hostname (App Server 2) or IP address.

---

## 🧩 **Step 2 – Create the user with an expiry date**

### Command:

`sudo useradd -m -e 2024-04-15 javed`

### Explanation:

|Option|Meaning|
|---|---|
|**sudo**|Runs the command with admin privileges (needed for user management).|
|**useradd**|The command used to create a new user account.|
|**-m**|Creates a **home directory** for the user (e.g., `/home/javed`).|
|**-e 2024-04-15**|Sets the **account expiration date**. After midnight on that day, the account becomes inactive and cannot log in.|
|**javed**|The username — all lowercase as required.|

✅ After this, the user `javed` is created and will automatically expire on **April 15 2024**.

---

## 🧩 **Step 3 – Set a password for the new user**

`sudo passwd javed`

- **passwd** — Used to set or change a user’s password.
- You’ll be prompted to **enter and confirm** the new password.

✅ This makes the account usable (for example, if the developer needs to log in via SSH).

---

## 🧩 **Step 4 – Verify the account and expiry date**

`sudo chage -l javed`
### Explanation:

| Option    | Meaning                                                        |
| --------- | -------------------------------------------------------------- |
| **chage** | Displays or changes account password and expiry info.          |
| **-l**    | List the current settings (e.g., password aging, expiry date). |
| **javed** | The username to check.                                         |
### Raw Output:

![[Screenshot 2025-10-21 at 3.29.49 PM.png]]

✅ You should see a line like:
`Account expires : Apr 15, 2024`

---

## 🧩 **Step 5 – (Optional) Confirm in /etc/shadow**

`sudo grep javed /etc/shadow`

- `/etc/shadow` stores encrypted passwords and account expiry info.
- The **8th field** (counting `:` separators) is the expiry date in _days since 1 Jan 1970_. For 2024-04-15, that number should correspond to **~19972**.

_(This is just for confirmation, not usually required.)_

---

## 🧩 **Step 6 – (Optional) Test login**

You can test if the user works before expiry:

`su - javed`

- `su` — switch user.
- `-` — start a login shell.
- `javed` — target user.

Enter the password you set in Step 3.  
✅ It should log in normally.

After 2024-04-15, login will fail automatically with a message like:

>Your account has expired; please contact your system administrator.
>su: User account has expired