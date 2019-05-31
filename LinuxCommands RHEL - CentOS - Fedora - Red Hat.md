# LinuxCommands RHEL - CentOS - Fedora - Red Hat
in progress 👋

![CentOS-7-Installation](https://user-images.githubusercontent.com/22911613/58729303-5b117480-83e9-11e9-911a-6bf78fecef2c.jpeg)

**/// Change a server's hostname in CentOS ///**

- hostnamectl set-hostname hostname.domain.com


-----------------------------------------------------------

**/// Systemctl ///**

> Starting and Stopping Services

- sudo systemctl start application
- sudo systemctl stop application.service
- sudo systemctl restart application.service
- sudo systemctl reload application.service

> To start, disable a service at boot

- sudo systemctl enable application.service
- sudo systemctl disable application.service

> Checking the Status of Services

- systemctl status application.service

-----------------------------------------------------------

**/// Network ///**

- netstat
- netstat -tulpn
- ifconfig
- ifconfig eth0 192.168.1.5 netmask 255.255.255.0

-----------------------------------------------------------

**/// Manage OS updates ///**

- sudo yum check-update
- sudo yum list obsoletes
- sudo yum update
- sudo yum update --security
- cat /etc/redhat-release

-----------------------------------------------------------


**/// SELINUX ///**

> Checking the Current Status & Mode of SELinux

- sestatus

> Temporarily Disable SELinux on CentOS 7

- sudo setenforce 0 (permissive)
- sudo setenforce 1 (enforcing)

> Permanently Disable SELinux on CentOS 7

- sudo nano /etc/selinux/config
- to SELINUX=disabled

-----------------------------------------------------------

**/// SSH ///**

- yum install openssh-server
- service sshd start
- service sshd status
- systemctl start sshd
- ssh-keygen -t ed25519

> Connect on alternate port number

- ssh -p 1022 192.168.1.100

> Banner Messages

- https://www.tecmint.com/protect-ssh-logins-with-ssh-motd-banner-messages/


> Allow Group SSH

- sudo vi /etc/ssh/sshd_config

> Rajouter 

- AllowGroups sshusers

> Restart SSH

- sudo systemctl restart sshd

> SSH without password

- https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/

-----------------------------------------------------------

**/// PWD ///**

> Afficher le chemin d'accès

- pwd

-----------------------------------------------------------

**/// Touch ///**

> Créer un fichier

- touch fichier.txt

-----------------------------------------------------------

**/// VI ///**

> Éditer un fichier

- vi fichier.txt (e pour edit)

-----------------------------------------------------------

**/// Utilisateurs ///**

> Afficher les utilisateurs

- cat etc/passwd

> Afficher les groupes

- cat /etc/group


> Créer un utilisateur + mot de passe

- adduser user
- passwd user

>  Supprimer un utilisateur

- sudo userdel -r user

> Gestion des utilisateurs

- usermod L user (Désactiver un compte)
- usermod U user (Activer un compte)
- usermod -g GroupLocal NomUser (Changer l'utilisateur de groupe)
- usermod -aG GroupLocal NomUser (Changer l'utilisateur de groupe en gardant ces anciens groups)

> Ajouter un user dans un groupe

- gpasswd -a alex nom du groupe

-----------------------------------------------------------

**/// nmap ///**

> Scan ports

- nmap -sV ip

-----------------------------------------------------------

**/// fail2ban ///**

> Install fail2ban

- yum install fail2ban

> Configurer fail2ban

- cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
- vi /etc/fail2ban/jail.local
- systemctl enable fail2ban
- systemctl start fail2ban
- cat /var/log/fail2ban

https://doc.fedora-fr.org/wiki/SSH_:_Se_prot%C3%A9ger_des_attaques_avec_fail2ban

-----------------------------------------------------------

**/// firewalld ///**

> To start firewalld

- sudo systemctl start firewalld
- sudo systemctl enable firewalld

> To stop firewalld

- sudo systemctl stop firewalld
- sudo systemctl disable firewalld
- sudo systemctl mask firewalld

> Add a Role

- sudo firewall-cmd --permanent --add-service=http

> Open a port

- sudo firewall-cmd --permanent --add-por=443/tcp

> List ports and service

- sudo firewall-cmd --list-ports
- sudo firewall-cmd --list-services

> Reload firewaldd

- sudo firewall-cmd --reload

-----------------------------------------------------------

**/// Root ///**

- sudo passwd root

-----------------------------------------------------------

**/// Midnight Commander ///**

> Install Midnight Commander

- yum install mc
- mc

-----------------------------------------------------------

**/// iSCI ///**

**/// NTP ///**

**/// LDAP ///**

**/// BIND ///**

**/// NFS ///**

**/// SMB ///**

**/// SMTP ///**




