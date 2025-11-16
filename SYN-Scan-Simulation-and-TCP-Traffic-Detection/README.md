### SYN Scan Simulation and TCP Traffic Detection

### Exercise Objective

Simulate a TCP SYN port scan from a Kali Linux VM to a Xubuntu VM within a VirtualBox internal network. Capture and analyze the traffic in real time using `tcpdump`, in order to:

- Understand how SYN scans appear on the network.
    
- Identify how they can be detected from a defensive perspective.
    
- Practice documenting such activity in a SOC-style report.
    

---

###  Environment Used

- **Kali Linux VM** → IP `10.0.4.20`
    
- **Xubuntu VM** → IP `10.0.4.10`
    
- **VirtualBox Internal Network** → `10.0.4.0/24`
    
- **Tools** → `nmap`, `tcpdump`, `ip`, `ping`
    

---

### Detailed Steps

#### 🔹 Step 1: Connectivity Check

**Commands:**

`ping 10.0.4.10  # From Kali ping 10.0.4.20  # From Xubuntu`

**Purpose:** verify that both VMs can communicate within the subnet.

![Ping Kali](01-Screen-Ping-Kali.png)

![Ping Xubuntu](02-Screen-Ping-Xub.png)

#### 🔹 Step 2: Identify Network Interface

**Command:**

`ip a  # Executed on Xubuntu`

**Purpose:** determine which interface is attached to the internal network (e.g., `enp0s8`).

![IP Address Xubuntu](03-Screen-ip-Xub.png)

#### 🔹 Step 3: Start Traffic Capture

**Command:**

`sudo tcpdump -i enp0s8 -nn`

**Purpose:** capture incoming packets in real time, displaying raw IPs and ports.

---

#### 🔹 Step 4: Perform SYN Scan

**Command:**

`nmap -sS 10.0.4.10  # From Kali`

**Purpose:** simulate a TCP SYN stealth scan, sending SYN packets without completing the full three-way handshake.

![Nmap Scan from Kali](04-Screen-nmap-Kali.png)

#### 🔹 Step 5: Analyze Results

**Expected tcpdump output on Xubuntu:**

`IP 10.0.4.20.XXXXX > 10.0.4.10.YYYYY: Flags [S], ... IP 10.0.4.10.YYYYY > 10.0.4.20.XXXXX: Flags [R.], ...`

**Interpretation:**

- `Flags [S]` → Kali is attempting to initiate connection (SYN).
    
- `Flags [R.]` → Xubuntu responds with Reset → closed port.
    
- `Flags [S.]` or `Flags [S,ACK]` → would indicate an open port.

 ![Scan Results on Xubuntu](05-Screen-Results-Xub-.png)

 ![Scan Results on Kali](06-Screen-Results-Kali.png)

###  Conclusion

This lab reproduces a realistic scenario of network reconnaissance detection. It demonstrates how SYN scans create identifiable patterns visible with `tcpdump`, and how a SOC analyst can interpret them effectively.

---

### 📘 Lessons Learned

- SYN scans produce consistent and easily observable TCP patterns.
    
- Mastering TCP flags interpretation is essential for defensive monitoring.
    
- Documenting labs with screenshots and structured explanations strengthens a professional portfolio.
    
- Exercises like this reinforce skills relevant to **CompTIA Security+** certification and SOC/OT analyst roles.

