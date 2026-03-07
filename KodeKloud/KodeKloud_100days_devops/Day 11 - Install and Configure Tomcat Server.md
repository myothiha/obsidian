
## Assignment

The `Nautilus` application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in `Stratos DC`. After an internal team meeting, they have decided to use the `tomcat` application server. Based on the requirements mentioned below complete the task:  

a. Install `tomcat` server on `App Server 2`.  
b. Configure it to run on port `3000`.  
c. There is a `ROOT.war` file on `Jump host` at location `/tmp`.  
  

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e `curl http://stapp02:3000`

 ---
 
This task involves setting up a Java servlet container (Tomcat), reconfiguring its default networking, and deploying a web archive (WAR) file.

---

## **Step 1: Install Tomcat on App Server 2**

Log in to **App Server 2** (stapp02) and install the Tomcat package.

Bash

```
sudo yum install -y tomcat
```

### **Deep Dive: Commands & Options**

- **`yum install`**: The package manager utility for RHEL-based systems.
- **`-y`**: **Assume Yes.** Automatically answers "yes" to the confirmation prompt to download and install the package.

---

## **Step 2: Configure Tomcat to Port 3000**

By default, Tomcat runs on port **8080**. We need to modify the `server.xml` file.

1. Open the configuration file:
	Bash
    ```
    sudo vi /etc/tomcat/server.xml
    ```
    
2. Find the line that looks like this: `<Server port="8005" shutdown="SHUTDOWN">`
3. Change `8080` to `3000`.
4. Save and exit (`:wq`).

### **Deep Dive: Commands & Options**

- **`/etc/tomcat/server.xml`**: The main configuration file for the Tomcat server instance.
- **`Connector port`**: The attribute that defines which TCP port the server listens on for incoming HTTP requests.

---

## **Step 3: Transfer the ROOT.war File**

Go to the **Jump Host** and copy the file to App Server 2.

Bash

```
scp /tmp/ROOT.war tony@stapp02:/tmp/
```

### **Deep Dive: Commands & Options**

- **`scp` (Secure Copy)**: Uses SSH to move files between hosts.
    
- **`/tmp/ROOT.war`**: The source file on the Jump Host.
    
- **`tony@stapp02:/tmp/`**: The destination (User@Host:Directory) on App Server 2.
    

---

## **Step 4: Deploy the Application**

On **App Server 2**, move the file to the Tomcat webapps directory.

Bash

```
sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/
```

### **Deep Dive: Commands & Options**

- **`/var/lib/tomcat/webapps/`**: The default deployment directory. When Tomcat sees a `.war` file here, it automatically "unpacks" it and starts the application.
    
- **`ROOT.war`**: Naming the file `ROOT` (case-sensitive) ensures the application is served at the base URL (`/`) rather than a sub-path (like `/ROOT`).
    

---

## **Step 5: Start and Enable Tomcat**

Now, start the service so the changes take effect.

Bash

```
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

### **Deep Dive: Commands & Options**

- **`systemctl start`**: Immediately starts the Tomcat background process.
    
- **`systemctl enable`**: Configures the service to start automatically if the server reboots.
    

---

## **Step 6: Verification**

Test if the website is accessible on the new port.

Bash

```
curl http://stapp02:3000
```

> **Note:** If the command fails, ensure the `ROOT` folder was created inside `/var/lib/tomcat/webapps/`. Tomcat sometimes needs a few seconds to "auto-deploy" the file after starting.

**Would you like me to show you how to check the Tomcat logs in case the application fails to start?**