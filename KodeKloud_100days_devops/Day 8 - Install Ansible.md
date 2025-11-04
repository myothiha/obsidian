
# Assignment

During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with `Ansible` for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use `jump host` as an Ansible controller to test different kind of tasks on rest of the servers.  

Install `ansible` version `4.10.0` on `Jump host` using `pip3` only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

---
# Solution

## 🧩 **Step 1 — Connect to the Jump Host**

`ssh thor@jump_host.stratos.xfusioncorp.com`

- **User:** `thor`
- **Password:** `mjolnir123`

---

## 🧩 **Step 2 — Check Python3 and pip3 installation**

We’ll ensure Python 3 and pip3 are available (they are required for Ansible via pip).

```
python3 --version
pip3 --version
```

### Expected:

`Python 3.x.x pip 20.x (python 3.x)`

If pip3 is missing:

```
sudo yum install -y python3-pip
```

|Option|Meaning|
|---|---|
|**yum**|Package manager (RHEL/CentOS).|
|**install -y python3-pip**|Installs pip for Python 3, automatically confirming prompts.|

---

## 🧩 **Step 3 — Install Ansible version 4.10.0 globally**

We’ll install using `pip3` with the `--prefix /usr/local` option to make it available to all users.

```
sudo pip3 install ansible==4.10.0 --prefix /usr/local
```

### Explanation:

|Option|Meaning|
|---|---|
|**sudo**|Install system-wide with admin privileges.|
|**pip3**|Python 3 package installer.|
|**install ansible==4.10.0**|Installs that exact version of Ansible.|
|**--prefix /usr/local**|Ensures the package binaries go into `/usr/local/bin` — a path accessible to **all users** globally.|

✅ Expected output (snippet):

`Successfully installed ansible-4.10.0 ...`

---

## 🧩 **Step 4 — Verify installation**

```
ansible --version
```

✅ Expected output:

`ansible [core 2.11.10]   config file = None   python version = 3.x.x`

This confirms Ansible 4.10.0 (core 2.11.10) is installed.

---

## 🧩 **Step 5 — Ensure global availability**

To make sure **all users** can access the Ansible binary, check where it’s installed:

`which ansible`

Typical result:

`/usr/local/bin/ansible`

If `/usr/local/bin` isn’t in every user’s `$PATH`, add it system-wide:

```
echo 'export PATH=$PATH:/usr/local/bin' | sudo tee /etc/profile.d/ansible_path.sh sudo chmod +x /etc/profile.d/ansible_path.sh
```

|Command|Meaning|
|---|---|
|**echo 'export PATH=...'|Creates a script that adds `/usr/local/bin` to global PATH.|
|**tee /etc/profile.d/...**|Writes it to a file that loads for all users on login.|
|**chmod +x**|Makes that file executable.|

Now every user who logs in will automatically have Ansible commands in their path.

---

## 🧩 **Step 6 — Verify as another user (optional)**

If another user exists (e.g., root), test:

```
sudo su - root
ansible --version
```

✅ You should still see:

`ansible [core 2.11.10]`

---

## ✅ **Summary**

| Step | Command                                                 | Description              |
| ---- | ------------------------------------------------------- | ------------------------ |
| 1    | `ssh thor@jump_host.stratos.xfusioncorp.com`            | Connect to Jump Host     |
| 2    | `python3 --version`, `pip3 --version`                   | Check Python/pip         |
| 3    | `sudo pip3 install ansible==4.10.0 --prefix /usr/local` | Install Ansible globally |
| 4    | `ansible --version`                                     | Verify version           |
| 5    | `which ansible`                                         | Confirm global path      |
| 6    | `echo 'export PATH=...'                                 | tee /etc/profile.d/...`  |
