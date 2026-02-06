
# Assignment

In response to heightened security concerns, the `xFusionCorp Industries` security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications:  

a. Create a user named `rose` on `App server 3` within the Stratos Datacenter.  
b. Assign a unique UID `1620` and designate the home directory as `/var/www/rose`.

> Note: You can find the infrastructure details by clicking on the **Details of all Users and Servers** button on the top-right section of the page.


# Solution

## Step 1: Access App Server 3

Before running commands, you must ensure you are on the correct host. Based on typical KodeKloud/Stratos DC setups, you usually SSH from the jump host.

- **Command:** `ssh banner@stapp03` (or the specific IP provided in your "Details" tab).
- **Purpose:** To gain shell access to the specific application server where the user needs to be created.

---

## Step 2: Create the User with Specifications

We will use the `useradd` command to create the user `rose` with the specific UID and home directory in a single step.

### The Command

```
sudo useradd -u 1620 -d /var/www/rose -m rose
```

### The "Nitty-Gritty" Explanation

|**Flag / Option**|**Description**|**Purpose in this Task**|
|---|---|---|
|**`sudo`**|SuperUser Do|User creation is a privileged task. You need root-level permissions to modify `/etc/passwd`.|
|**`useradd`**|The binary command|This is the standard utility used to create a new low-level user.|
|**`-u 1620`**|User ID (UID)|Overrides the default auto-increment. It ensures `rose` has the exact ID of **1620** as requested.|
|**`-d /var/www/rose`**|Home Directory|Sets the path for the user's home. Since this is for Apache, we point it to the web directory.|
|**`-m`**|Create Home|This flag tells Linux to actually **create** the directory `/var/www/rose`. Without this, the path is set in settings but the folder won't exist.|
|**`rose`**|Username|The final argument specifies the name of the account being created.|

---

## Step 3: Verify the Creation

It is best practice to verify that the UID and directory were applied correctly.

### The Commands

1. **Check User Details:**
```
id rose
```

- **Explanation:** This returns the `uid`, `gid`, and `groups`. You should see `uid=1620(rose)`.

2. **Check Home Directory:**

```
ls -ld /var/www/rose
```

- **Explanation:** The `-d` flag tells `ls` to show the directory itself rather than its contents. This confirms the directory exists and is owned by `rose`.

---

### Important Note on Permissions

Since this is for an **Apache** setup, the security team might later ask you to adjust permissions so the web server can read these files. However, for _this_ specific assignment, completing the `useradd` command satisfies the requirements.