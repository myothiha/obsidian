
## Assignment

The system admin team at `xFusionCorp Industries` has streamlined access management by implementing group-based access control. Here's what you need to do:  

a. Create a group named `nautilus_noc` across all App servers within the `Stratos Datacenter`.  

b. Add the user `mohammed` into the `nautilus_noc` group on all App servers. If the user doesn't exist, create it as well.

---

## Solution

Since you are working across multiple App servers in the Stratos Datacenter (typically `stapp01`, `stapp02`, and `stapp03`), you will need to perform these steps on each server.

Here is the step-by-step guide to fulfilling the group and user requirements:

---

### Step 1: Create the Group

The first requirement is to ensure the specific group exists so it can be used for access control.

Bash

```
sudo groupadd nautilus_noc
```

- **`sudo`**: Runs the command with root privileges, which is required for modifying system files like `/etc/group`.
- **`groupadd`**: The standard binary used to create a new group definition in the system.
- **`nautilus_noc`**: The specific name of the group requested in the challenge.

---

### Step 2: Create or Update the User

You need to ensure the user `mohammed` exists and is a member of the new group. The following command handles both the creation (if missing) and the group assignment.

Bash

```
sudo id mohammed || sudo useradd mohammed
```

- **`id mohammed`**: Checks if the user already exists.
- **`||`**: A logical OR operator. It ensures that the second command (`useradd`) only runs if the first command fails (i.e., the user does not exist).
- **`useradd`**: Creates a new high-level user account.

---

### Step 3: Add the User to the Group

Once the group and user both exist, you must link them. Using the `-aG` flags ensures you don't accidentally remove the user from any other groups they might already belong to.

Bash

```
sudo usermod -aG nautilus_noc mohammed
```

- **`usermod`**: Modifies an existing user's system settings.
- **`-a` (append)**: This is crucial; it adds the user to the new group without removing them from their current primary or secondary groups.    
- **`-G` (groups)**: Specifies the supplementary group(s) that the user will be added to.

---

### Step 4: Verify the Changes

It is a best practice in KodeKloud challenges to verify your work before hitting the "Check" button.

Bash

```
id mohammed
```

- **`id`**: Displays the UID (User ID), GID (Primary Group ID), and any supplementary groups.
- **Expected Output**: You should see `nautilus_noc` listed under the `groups=` section of the output.

---

Would you like me to show you how to automate this across all three App servers using a single loop, or should we stick to manual entry for now?