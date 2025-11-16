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

        `Internal Network: intnet (10.232.231.0/24) ┌───────────────┐                     ┌───────────────┐ │   Kali Linux  │                     │   Xubuntu     │ │ 10.232.231.73 │◀────── Ping/SSH ──▶│ 10.232.231.74 │ │  eth1: intnet │                     │ enp0s3: intnet│ └───────────────┘                     └───────────────┘`


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

