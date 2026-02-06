To accommodate the backup agent tool's specifications, the system admin team at `xFusionCorp Industries` requires the creation of a user with a non-interactive shell. Here's your task:  
  
Create a user named `john` with a non-interactive shell on `App Server 1`.

> Note: You can find the infrastructure details by clicking on the **Details of all Users and Servers** button on the top-right section of the page.
---
# Solution

### Quick recap

1. Ensure `/sbin/nologin` exists.
2. `useradd -m -s /sbin/nologin john` (create user with non-interactive shell).
3. _(Optional)_ `passwd -l john` (lock password) — **skip for now** if you plan to test with a temporary password.
4. `passwd john` (set temporary password) → _(unlock first with `passwd -u john` if needed)_.
5. `grep john /etc/passwd` (confirm shell).
6. `su - john` (verify it’s blocked by `nologin`).
7. `passwd -l john` (lock again) **or** `passwd -d john` (delete password; less safe).
8. `getent passwd john` (optional verification).

---
### 1 - Confirm a non-interactive shell exists

`ls -l /sbin/nologin /usr/sbin/nologin /bin/false 2>/dev/null`

- `ls -l` — list files in long format (permissions, owner, path).
- `/sbin/nologin /usr/sbin/nologin /bin/false` — common non-interactive shells.
- `2>/dev/null` — hides error messages if a path doesn’t exist.

✅ If /sbin/nologin exists, we’ll use it (preferred).

---
## 2) Create the user with a non-interactive shell

`sudo useradd -m -s /sbin/nologin john`

- `sudo` — run with admin privileges (needed to manage users).
- `useradd` — creates a new user account.
- `-m` — create the user’s home directory (e.g., `/home/john`); safe/typical default.
- `-s /sbin/nologin` — set login shell to **non-interactive** (blocks interactive sessions).
- `john` — the username.

> Alternative shell if needed: `-s /bin/false` (also blocks login, but is silent).

---
## 3) (Optional) Lock the password for extra safety

`sudo passwd -l john`

- `passwd` — manage user passwords.
- `-l` — **lock** the password (prefixes it to prevent password auth).

> Not strictly required since `/sbin/nologin` already blocks shell access, but it hardens the account. You can **skip this now** if you plan to set a temporary password in the next step. If you already ran it, you’ll need to **unlock** before setting a new password (see Step 4b).

---
## ## 4) (New) Set a temporary password so you can test `su`

`sudo passwd john`

- `passwd john` — set (or change) `john`’s password interactively (you’ll be prompted twice).

**If you previously locked the password in Step 3**, unlock first:

`sudo passwd -u john`

- `-u` — **unlock** the password (reverses `-l`).

---

## 5) Verify the shell is non-interactive in `/etc/passwd`

`grep john /etc/passwd`

- `grep john` — search for `john`.
- `/etc/passwd` — user database (username, UID/GID, home, shell).

✅ Expect the last field to be `/sbin/nologin`, e.g.:

`john:x:1002:1002::/home/john:/sbin/nologin`

---

## 6) Try switching to the user (will be blocked by nologin)

`su - john`

- `su` — switch user.
- `-` — start a **login** shell (full environment).
- `john` — target user.

🔒 Expected:

- With `/sbin/nologin`: `This account is currently not available.`
- With `/bin/false`: it returns to your shell immediately (no message).

> The **password prompt** is normal—`su` asks for the **target user’s** password.  
> If you run `sudo su - john`, it won’t ask for `john`’s password (because you’re root), but `nologin` will still block the session.

---

## 7) (New) Remove/disable the password again after testing

**Recommended (safer): Lock the password**

`sudo passwd -l john`

- `-l` — **lock** password auth (cannot be used to log in with a password).

**Alternative (not recommended on most systems): Delete the password**

`sudo passwd -d john`

- `-d` — **delete** the password hash (sets it empty).  
    ⚠️ On some PAM configs with `nullok`, an empty password might allow login; this is why **locking** is safer.

**(Either way) `nologin` still blocks interactive shells**. Locking is just extra hardening.

---

## 8) (Optional) Cross-check via system database

`getent passwd john`

- `getent` — query system databases.
- `passwd` — the user accounts database.
- `john` — entry to retrieve.

Output should again end with `/sbin/nologin`.

---

