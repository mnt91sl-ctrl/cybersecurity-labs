🛡️ Linux ACL Simulation
🎯 Experiment Context
Environment: Xubuntu on Oracle VirtualBox Goal: Configure granular access control over /security using ACLs (Access Control Lists).

1️⃣ Create a Security Group
sudo groupadd securitygrp

2️⃣ Create Users and Assign Full Names
sudo adduser secadmin   # Full Name: Patricio Rey
sudo adduser secanalyst # Full Name: Security Analyst
sudo adduser guestsec   # Full Name: Security Guest
![Screenshot 1](evidence/Screenshot-Xub-1.png)

3️⃣ Add Users to the securitygrp Group
sudo usermod -aG securitygrp secadmin
sudo usermod -aG securitygrp secanalyst
sudo usermod -aG securitygrp guestsec

4️⃣ Create the Protected Directory
sudo mkdir /security
sudo chown root:securitygrp /security
sudo chmod 770 /security  # Base permissions: rwx for owner and group

5️⃣ Apply User-Specific ACLs
sudo setfacl -m u:secadmin:rwx /security      # Full access
sudo setfacl -m u:secanalyst:r-x /security    # Read and execute only
sudo setfacl -m u:guestsec:r-- /security      # Read only
sudo setfacl -m m::r-x /security              # Restrictive mask

6️⃣ Verify Configuration
getfacl /security
ls -ld /security

7️⃣ Practical Tests by User
su - secadmin -c "touch /security/adminfile.txt && echo 'Admin test' > /security/adminfile.txt"

su - secanalyst -c "touch /security/analystfile.txt && echo 'Analyst test' > /security/analystfile.txt"

su - guestsec -c "touch /security/guestfile.txt && echo 'Guest test' > /security/guestfile.txt"

📊 Skills Demonstrated
✅ Linux user and group management

✅ Directory permission hardening

✅ Granular ACL configuration

✅ Practical validation of access rights

⚠️ Ethical Note
This lab was conducted in a controlled environment for educational and professional development purposes. Unauthorized use of these techniques on live systems without consent is illegal and unethical. As cybersecurity professionals, we must apply our skills responsibly to protect systems, not exploit them.

