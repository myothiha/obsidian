
# Assignment

The production support team of `xFusionCorp Industries` is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on `App Server 2` in `Stratos Datacenter`, and they need to create a bash script named `official_backup.sh` which should accomplish the following tasks. (Also remember to place the script under `/scripts` directory on `App Server 2`).  
  
a. Create a zip archive named `xfusioncorp_official.zip` of `/var/www/html/official` directory. 
b. Save the archive in `/backup/` on `App Server 2`. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on `Nautilus Backup Server`.  
c. Copy the created archive to `Nautilus Backup Server` server in `/backup/` location.  
d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, `tony` in case of `App Server 1`) must be able to run it. 
e. Do not use sudo inside the script.

**Note:**  
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.


# Solution

### **Step 1: Install the Zip Utility**

The instructions explicitly state that `zip` must be installed manually before running the script.

Bash

```
sudo yum install -y zip
```

- **`yum`**: The package manager for RHEL/CentOS systems (common in Stratos DC).
- **`install -y`**: Tells the system to install the package and automatically answer "yes" to any confirmation prompts.

---

### **Step 2: Set Up Passwordless SSH**

Requirement **(d)** states the script must not ask for a password. We achieve this using SSH keys.

1. **Generate the key pair:**

```
ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa
```

- **`-t rsa`**: Specifies the RSA encryption algorithm.
- **`-N ""`**: Sets an empty passphrase (so the _key_ doesn't ask for a password either).
- **`-f ...`**: Specifies the filename/location for the key.

1. **Copy the key to the Backup Server:** _(Assuming the backup user is **clint** and the host is **stbkp01** based on standard Nautilus lab naming—check your specific lab credentials)_.

```
ssh-copy-id clark@stbkp01
```

- **`ssh-copy-id`**: This utility "registers" your public key on the backup server. You'll enter the password one last time here; after this, no password is required.

---

### **Step 3: Create the Script Directory and File**

Requirement **(e)** says do not use `sudo` _inside_ the script, but we need `sudo` now to create the directory.

```
sudo mkdir -p /scripts /backup
sudo touch /scripts/official_backup.sh
sudo chmod 755 /scripts/official_backup.sh
sudo chown steve:steve /scripts/official_backup.sh 
```

- **`mkdir -p`**: The "parent" flag ensures the command creates the folder even if the parent directory doesn't exist yet.
- **`chmod 755`**: Sets permissions so the owner can read/write/execute, and others can read/execute. This satisfies the requirement that the server user can run it.
- **`chown`**: Changes the owner to your current lab user (e.g., `steve` or `tony`) so you can edit it without `sudo`.

---

### **Step 4: Write the Script Content**

Open the file: `vi /scripts/official_backup.sh` and enter the following:

```
#!/bin/bash

# a. & b. Create zip archive and save in /backup/
zip -r /backup/xfusioncorp_official.zip /var/www/html/official

# c. Copy the archive to Nautilus Backup Server
scp /backup/xfusioncorp_official.zip clint@stbkp01:/backup/
```

#### **Explanation of Script Commands:**

- **`#!/bin/bash`**: This "Shebang" tells the kernel to use the Bash shell to interpret these commands.
- **`zip -r`**:
    - **`-r` (Recursive)**: This is crucial. It tells `zip` to include all files and subdirectories inside `/official`. If you omit this, you'll just get an empty folder in your zip.
- **`scp` (Secure Copy)**:
    - This uses the SSH protocol to copy the file. Because we did **Step 2**, this command will execute silently without prompting for a password.

---

### **Step 5: Final Execution and Verification**

Run the script as your normal user:

```
/scripts/official_backup.sh
```

**To verify:**

1. Check local: `ls -l /backup/xfusioncorp_official.zip`
2. Check remote: `ssh clark@stbkp01 "ls -l /backup/xfusioncorp_official.zip"`

---

### **Summary of Requirements Met:**

- **Zip installed?** Yes (Step 1).
- **Script name/location?** `/scripts/official_backup.sh` (Step 3).
- **Archive name?** `xfusioncorp_official.zip` (Step 4).
- **No password?** Yes, via SSH keys (Step 2).
- **No sudo inside script?** Yes, we used direct paths and proper ownership.