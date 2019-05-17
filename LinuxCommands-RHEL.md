# LinuxCommands RHEL - CentOS - Fedora - Red Hat
in progress

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

> Créer un utilisateur + mot de passe

- adduser user
- passwd user

> Gestion des utilisateurs

- usermod L user (Désactiver un compte)
- usermod U user (Activer un compte)
- usermod -g GroupLocal NomUser (Changer l'utilisateur de groupe)
- usermod -aG GroupLocal NomUser (Changer l'utilisateur de groupe en gardant ces anciens groups)


-----------------------------------------------------------

**/// nmap ///**

- nmap -sV ip

-----------------------------------------------------------

**/// fail2ban ///**

> Install

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

> To stop firewalld

- sudo systemctl stop firewalld
- sudo systemctl disable firewalld
- sudo systemctl mask firewalld

-----------------------------------------------------------

/// How To Secure A Linux Server  ///

- https://github.com/imthenachoman/How-To-Secure-A-Linux-Server

-----------------------------------------------------------

**/// Passer en Root ///**

sudo passwd root
