# Man-in-the-Middle (MitM) Attack via ARP Spoofing and Packet Forwarding with Kali Linux

### 🎯 Objective

To demonstrate how to intercept traffic between a victim and a router using Kali Linux, by configuring the system as an intermediary through ARP spoofing, enabling IP forwarding, and capturing credentials using Wireshark.

---

### 🔹 Step 1: Launch Kali Linux in VirtualBox

Start the Kali Linux virtual machine using Oracle VirtualBox to conduct the test in a controlled environment.

---

### 🔹 Step 2: Enable IP Forwarding

#### Method A: Temporary Activation

Run the following command in the terminal to allow Kali to forward packets between interfaces:


```
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

![ARP Spoofing](Screenshot-Mitm-1.png)

#### Method B: Permanent Activation

Edit the system configuration file:

```
sudo nano /etc/sysctl.conf

net.ipv4.ip_forward=1

sudo sysctl -p
```

![Permanent IP Forwarding](Screenshot-Mitm-2.png)


