# LinuxCommands RHEL - CentOS - Fedora - Red Hat
 Learn, and save time - in progress 👋

![CentOS-7-Installation](https://user-images.githubusercontent.com/22911613/58729303-5b117480-83e9-11e9-911a-6bf78fecef2c.jpeg)

**/// Change a server's hostname in CentOS ///**

- ``` hostnamectl set-hostname hostname.domain.com```

-----------------------------------------------------------

**/// Root ///**

- ```sudo passwd root ```

-----------------------------------------------------------

**/// Manage OS updates ///**

- ``` sudo yum check-update ```
- ``` sudo yum list obsoletes ```
- ``` sudo yum update ```
- ``` sudo yum update --security ```
- ``` cat /etc/redhat-release ```

-----------------------------------------------------------

**/// Limit Who Can Use sudo ///**

Create a group

- ``` sudo groupadd sudousers ```

Add account to the group:

- ``` sudo usermod -a -G sudousers user1 ```

Make a backup of the sudo's configuration file /etc/sudoers:

- ``` sudo cp --preserve /etc/sudoers /etc/sudoers.$(date +"%Y%m%d%H%M%S") ```

Edit sudo's configuration file /etc/sudoers:

- ``` sudo visudo ``` 

Tell sudo to only allow users in the sudousers group to use sudo by adding this line if it is not already there:

- ``` %sudousers   ALL=(ALL:ALL) ALL ```

**/// SSH ///**

- ``` yum install openssh-server ```
- ``` service sshd start ```
- ``` service sshd status ```
- ``` systemctl start sshd ```
- ``` ssh-keygen -t ed25519 ```

Acces SSHD Config

- ```sudo vi /etc/ssh/sshd_config ```

Create a group

- ```sudo groupadd sshusers ```

Add account to the group:

- ``` sudo usermod -a -G sshusers user1 ```

Make a backup of OpenSSH server's configuration file /etc/ssh/sshd_config

- ``` sudo cp --preserve /etc/ssh/sshd_config /etc/ssh/sshd_config.$(date +"%Y%m%d%H%M%S") ```
- ``` sudo sed -i -r -e '/^#|^$/ d' /etc/ssh/sshd_config ```

Restart SSH

- ``` sudo systemctl restart sshd ```

Connect on alternate port number

- ```ssh -p 1022 192.168.1.100 ```

Banner Messages

- https://www.tecmint.com/protect-ssh-logins-with-ssh-motd-banner-messages/

SSH without password

- https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/

-----------------------------------------------------------

**/// fail2ban ///**

Install fail2ban

- ``` yum install epel-release ```
- ``` yum install fail2ban fail2ban-systemd ```
- ``` yum update -y selinux-policy* ```

Configurer fail2ban

- ``` cp -pf /etc/fail2ban/jail.conf /etc/fail2ban/jail.local ```
- ``` nano /etc/fail2ban/jail.local ```

Add a jail file to protect SSH.

- ``` nano /etc/fail2ban/jail.d/sshd.local``` 

[sshd]
enabled = true
port = ssh
#action = firewallcmd-ipset
logpath = %(sshd_log)s
maxretry = 5
bantime = 86400

- ``` systemctl enable fail2ban ```
- ``` systemctl start fail2ban ```
- ``` cat /var/log/fail2ban ```

Check the Fal2Ban Status

- ``` fail2ban-client status ```

https://www.howtoforge.com/tutorial/how-to-install-fail2ban-on-centos/

-----------------------------------------------------------

**/// firewalld ///**

To start firewalld

- ``` sudo systemctl start firewalld ```
- ``` sudo systemctl enable firewalld ```

To stop firewalld

- ``` sudo systemctl stop firewalld ```
- ``` sudo systemctl disable firewalld ```
- ``` sudo systemctl mask firewalld ```

Add a Role

- ``` sudo firewall-cmd --permanent --add-service=http ```

Open a port

- ``` sudo firewall-cmd --permanent --add-port=443/tcp ```
- ```firewall-cmd --zone=public --add-port=22/tcp --permanent ```

List ports and service

- ``` sudo firewall-cmd --list-ports ```
- ``` sudo firewall-cmd --list-services ```

Reload firewaldd

- ```sudo firewall-cmd --reload ```

-----------------------------------------------------------

**/// ntp ///**

Install NTP

- ``` sudo yum install ntp ```
- ``` sudo systemctl start ntpd ```
- ``` sudo systemctl enable ntpd ```
- ``` sudo firewall-cmd --permanent --add-service=ntp ```
- ``` sudo firewall-cmd --reload ```

Check ntp's status:
- ``` sudo ntpq -p ```

**/// BIND ///**

Install BIND

- ```sudo yum install bind bind-utils ```

https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-centos-7

-----------------------------------------------------------

**/// Systemctl ///**

Starting and Stopping Services

- ``` sudo systemctl start application ```
- ``` sudo systemctl stop application.service ```
- ``` sudo systemctl restart application.service ```
- ``` sudo systemctl reload application.service ```

To start, disable a service at boot

- ``` sudo systemctl enable application.service ```
- ``` sudo systemctl disable application.service ```

Checking the Status of Services

- ``` systemctl status application.service ```

-----------------------------------------------------------

**/// Network ///**

- ``` netstat ```
- ``` netstat -tulpn ```
- ``` ifconfig ```
- ``` ifconfig eth0 192.168.1.5 netmask 255.255.255.0 ```

-----------------------------------------------------------

**/// SELINUX ///**

Checking the Current Status & Mode of SELinux

- ``` sestatus ```

Temporarily Disable SELinux on CentOS 7

- ``` sudo setenforce 0 (permissive) ```
- ``` sudo setenforce 1 (enforcing) ```

Permanently Disable SELinux on CentOS 7

- ``` sudo nano /etc/selinux/config ```
- to SELINUX=disabled

-----------------------------------------------------------

**/// PWD ///**

Afficher le chemin d'accès

- ```pwd ```

-----------------------------------------------------------

**/// Touch ///**

Create a file

- ``` touch fichier.txt ```

-----------------------------------------------------------

**/// VI ///**

Change a file

- ``` vi fichier.txt (e pour edit) ```

-----------------------------------------------------------

**/// Utilisateurs ///**

Afficher les utilisateurs

- ``` cat etc/passwd ```

Afficher les groupes

- ``` cat /etc/group ```


Créer un utilisateur + mot de passe

- ``` adduser user ```
- ``` passwd user ```

Supprimer un utilisateur

- ``` sudo userdel -r user ```

Gestion des utilisateurs

- ``` usermod L user (Désactiver un compte) ```
- ``` usermod U user (Activer un compte) ```
- ``` usermod -g GroupLocal NomUser (Changer l'utilisateur de groupe) ```
- ``` usermod -aG GroupLocal NomUser (Changer l'utilisateur de groupe en gardant ces anciens groups) ```

Ajouter un user dans un groupe

- ``` gpasswd -a alex nom du groupe ```

-----------------------------------------------------------

**/// nmap ///**

Scan ports

- ``` nmap -sV ip ```

-----------------------------------------------------------

**/// Midnight Commander ///**

Install Midnight Commander

- ``` yum install mc ```
- ``` mc ```

-----------------------------------------------------------
