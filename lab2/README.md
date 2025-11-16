Lab 02 — Linux ACL Simulation

Environment: Xubuntu on Oracle VirtualBox
Goal: Configure granular access control over /security using ACLs (Access Control Lists).

sudo groupadd securitygrp

sudo adduser secadmin      # Full Name: Patricio Rey
sudo adduser secanalyst    # Full Name: Security Analyst
sudo adduser guestsec      # Full Name: Security Guest
![User Creation](evidence/lab2/Screenshot Xub 1.png)

sudo usermod -aG securitygrp secadmin
sudo usermod -aG securitygrp secanalyst
sudo usermod -aG securitygrp guestsec
![Add to Group](evidence/lab2/Screenshot Xub2.png)

sudo mkdir /security
sudo chown root:securitygrp /security
sudo chmod 770 /security     # Base permissions: rwx for owner and group
![Directory Creation](evidence/lab2/Screenshot Xub3.png)

sudo setfacl -m u:secadmin:rwx /security          # Full access
sudo setfacl -m u:secanalyst:r-x /security        # Read + execute
sudo setfacl -m u:guestsec:r-- /security          # Read only
sudo setfacl -m m::r-x /security                  # Restrictive mask

getfacl /security
ls -ld /security

su - secadmin -c "touch /security/adminfile.txt && echo 'Admin test' > /security/adminfile.txt"

su - secanalyst -c "touch /security/analystfile.txt && echo 'Analyst test' > /security/analystfile.txt"

su - guestsec -c "touch /security/guestfile.txt && echo 'Guest test' > /security/guestfile.txt"
![User Tests](evidence/lab2/Screenshot Xub4.png)
