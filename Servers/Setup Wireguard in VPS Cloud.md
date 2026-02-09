**Note: Works on Ubuntu 24.04**
### Phase 1: Install WireGuard

First, we need the software on both ends.

- **On Ubuntu:**

```
sudo apt update && sudo apt install wireguard -y
```

- **On MacBook:** Download and install **WireGuard** from the Mac App Store.

---

### Phase 2: Generate Keys

WireGuard uses public/private key pairs. The private key stays on the device; the public key is shared with the "peer."

**On Ubuntu:**

```
wg genkey | sudo tee /etc/wireguard/private.key
sudo chmod 600 /etc/wireguard/private.key
sudo cat /etc/wireguard/private.key | wg pubkey | sudo tee /etc/wireguard/public.key
```

**On MacBook:**

1. Open the WireGuard app.
2. Click **Add Empty Tunnel**.
3. It will automatically generate a Public and Private key for you. **Copy the Public Key**; you'll need it for the server config.

---
### Phase 3: Configure the Server (Ubuntu)

Create the configuration file:

```
sudo nano /etc/wireguard/wg0.conf
```

Paste the following, replacing the placeholders:

Ini, TOML

```
[Interface]
PrivateKey = <Contents_of_Ubuntu_private.key>
Address = 10.0.0.1/24
ListenPort = 51820
SaveConfig = true

# This is your MacBook
[Peer]
PublicKey = <Your_MacBook_Public_Key>
AllowedIPs = 10.0.0.2/32
```

**Enable IP Forwarding** (so the server can route traffic):

```
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

**Start the Server:**

```
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
```

---

### Phase 4: Configure the Client (MacBook)

Go back to that "Empty Tunnel" window in your Mac app and fill it out like this:

Ini, TOML

```
[Interface]
PrivateKey = <Your_MacBook_Private_Key_Already_There>
Address = 10.0.0.2/24
DNS = 1.1.1.1

[Peer]
PublicKey = <Your_Ubuntu_Public_Key>
Endpoint = <Your_VPS_Public_IP>:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

> **Note:** Setting `AllowedIPs = 10.0.0.0/24` means only traffic intended for your private network goes through the VPN. If you want _all_ your Mac's internet traffic to go through the VPS, change it to `0.0.0.0/0`.

---

### Phase 5: Open the Firewall

For the connection to "handshake," your VPS must allow UDP traffic on the port we chose.

**On Ubuntu (assuming UFW):**

```
sudo ufw allow 51820/udp
```

### Testing the connection

On your Mac, click **Activate**. Then, open your terminal and try to ping the server's private IP: `ping 10.0.0.1`

If you get a response, you are officially inside your own private, free, and unlimited network.

---
# Add Another Computer to VPN

### Step 1: Generate Keys for Computer #2

Install the WireGuard app on your second computer.

- **If it's Windows/Mac:** Open the app, click **Add Tunnel** > **Add Empty Tunnel**. It will generate a Public and Private key.
    
- **If it's Linux:** Run the same commands we used for the Ubuntu server:
```
wg genkey | tee private.key | wg pubkey > public.key
```

---
### Step 2: Update the Server (Ubuntu)

You must tell your Ubuntu server that this second computer is allowed to connect.

1. Open your server config:
    `sudo nano /etc/wireguard/wg0.conf`
2. Add a **second** `[Peer]` section at the bottom. **Crucial:** You must give this computer its own unique IP (e.g., `10.0.0.3`).

Ini, TOML

```
# ... existing server and MacBook configs ...

# This is Computer #2
[Peer]
PublicKey = <Computer_2_Public_Key>
AllowedIPs = 10.0.0.3/32
```

3. Apply the changes without dropping existing connections:

```
sudo wg addconf wg0 <(printf "[Peer]\nPublicKey = <Computer_2_Public_Key>\nAllowedIPs = 10.0.0.3/32")
```

Alternatively, just restart the service: `sudo systemctl restart wg-quick@wg0`


---

### Step 3: Configure Computer #2

Set up the client config on the second computer. It looks almost identical to your MacBook config, but with a different IP and its own private key.

Ini, TOML

```
[Interface]
PrivateKey = <Computer_2_Private_Key>
Address = 10.0.0.3/24
DNS = 1.1.1.1

[Peer]
PublicKey = <Ubuntu_Server_Public_Key>
Endpoint = <Your_VPS_Public_IP>:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

---

### Summary Table of IP Assignments

|**Device**|**Role**|**WireGuard Private IP**|
|---|---|---|
|**Ubuntu VPS**|Server|`10.0.0.1`|
|**MacBook**|Client 1|`10.0.0.2`|
|**Second PC**|Client 2|`10.0.0.3`|