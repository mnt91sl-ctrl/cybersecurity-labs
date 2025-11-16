# Virtual Lab Documentation: Kali Linux & Xubuntu Internal Network

## Objective

Set up an isolated internal network in VirtualBox with Kali Linux and Xubuntu. Perform host discovery and service enumeration using Nmap to establish a baseline for services and connectivity. Document all steps for technical portfolio purposes.

---

## Lab Setup

### Kali Linux VM – Attacker / Scanner

- **Internal Network IP:** `10.232.231.73`
    
- **Interfaces:** `eth1 → intnet`
    

### Xubuntu VM – Target / Lab machine

- **Internal Network IP:** `10.232.231.74`
    
- **Interfaces:** `enp0s3 → intnet`
    

### Network Configuration

- **Adapter 1:** Internal Network → Kali ↔ Xubuntu
    
- **Adapter 2:** NAT (optional for Internet access / software installation)
    

**Diagram of Internal Network (ASCII):**

        Internal Network: intnet (10.232.231.0/24) ┌───────────────┐                     ┌───────────────┐ │   Kali Linux  │                     │   Xubuntu     │ │ 10.232.231.73 │◀────── Ping/SSH ──▶│ 10.232.231.74 │ │  eth1: intnet │                     │ enp0s3: intnet│ └───────────────┘                     └───────────────┘


---

## Step 1: Host Discovery (Kali Linux)

**Command executed:**

`nmap -sn 10.232.231.0/24 -oN 01_hosts_up.txt`

**Description:**  
Perform a ping sweep to detect active hosts in the `10.232.231.0/24` network. Hosts discovered include Kali itself, Xubuntu, and other devices in the network.

**Summary of Active Hosts:**

|IP|Hostname/Device|Host Up|
|---|---|---|
|10.232.231.73|Kali Linux|Yes|
|10.232.231.74|Xubuntu|Yes|
|10.232.231.113|Other Host|Yes|
|10.232.231.137|Other Host|Yes|

**Capture Reference:** Kali terminal showing ping sweep results.

![Nmap SYN Scan from Kali](01-Scan-Nmap-Kali.png)

## Step 2: Service Enumeration (Kali → Xubuntu)

**Command executed:**

`sudo nmap -sV -O -Pn 10.232.231.74 -oN 02_xubuntu_baseline.txt`

**Description:**  
Nmap detects open ports and services on Xubuntu. Only port 22 (SSH) is open with OpenSSH 9.6p1. OS detection identifies Linux 2.6.X (approximate).

**Summary of Detected Services:**

|Port|State|Service|Version / OS|
|---|---|---|---|
|22/tcp|open|ssh|OpenSSH 9.6p1 Ubuntu 3ubuntu13.13|
|OS detected|-|Linux 2.6.X (approximate)|CPE: cpe:/o:linux:linux_kernel:2.6.32|

**Capture Reference:** Xubuntu terminal showing Nmap scan results.

![Nmap SYN Scan from Xubuntu](02-Scan-Nmap-Xubuntu.png)

## Step 3: Notes and Recommendations

- Demonstrates basic network scanning and service enumeration in an isolated environment.
    
- Only essential services are exposed (SSH), ensuring a secure lab setup.
    
- Can be extended with hardening exercises, vulnerability scanning, or penetration testing labs.
    

---

## Step 4: Captures to Include

- **Kali Linux terminal:** Ping sweep (`nmap -sn`) and hosts detected.
    
- **Xubuntu terminal:** Nmap installation and service scan (`sudo nmap -sV -O -Pn`).
    

> Including screenshots visually confirms procedures and results for the portfolio.
