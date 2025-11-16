# 🧪 Lab 02: Linux ACL Simulation  
**Environment:** Xubuntu on Oracle VirtualBox  
**Goal:** Configure granular access control over `/security` using Linux **ACLs**.

---

## 1️⃣ Create a security group



2️⃣ Create users and assign full names
sudo groupadd securitygrp

sudo adduser secadmin       # Full Name: Patricio Rey
sudo adduser secanalyst     # Full Name: Security Analyst
sudo adduser guestsec       # Full Name: Security Guest
![Step 1](evidence/Screenshot-Xub-1.png)

3️⃣ Add users to the securitygrp group
sudo usermod -aG securitygrp secadmin
sudo usermod -aG securitygrp secanalyst
sudo usermod -aG securitygrp guestsec
![Group Assignment](../../evidence/lab2/Screenshot-Xub-2.png)

4️⃣ Create the protected directory
sudo mkdir /security
sudo chown root:securitygrp /security
sudo chmod 770 /security      # rwx for owner and group
![Directory Creation](../../evidence/lab2/Screenshot-Xub-3.png)

5️⃣ Apply user-specific ACLs
sudo setfacl -m u:secadmin:rwx /security      # Full access
sudo setfacl -m u:secanalyst:r-x /security    # Read + execute
sudo setfacl -m u:guestsec:r-- /security      # Read only
sudo setfacl -m m::r-x /security              # Restrictive mask

6️⃣ Verify configuration
getfacl /security
ls -ld /security

su - secadmin   -c "touch /security/adminfile.txt   && echo 'Admin test'   > /security/adminfile.txt"
su - secanalyst -c "touch /security/analystfile.txt && echo 'Analyst test' > /security/analystfile.txt"
su - guestsec   -c "touch /security/guestfile.txt   && echo 'Guest test'   > /security/guestfile.txt"
![ACL Tests](../../evidence/lab2/Screenshot-Xub-4.png)
