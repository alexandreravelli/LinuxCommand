# LinuxCommands RHEL - CentOS - Fedora - Red Hat
 Learn, and save time 👋
 in progress

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


-----------------------------------------------------------

**/// SSH ///**

- ``` yum install openssh-server ```
- ``` service sshd start ```
- ``` service sshd status ```
- ``` systemctl start sshd ```
- ``` ssh-keygen -t ed25519 ```

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
Created directory '/home/user/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/user/.ssh/id_ed25519.
Your public key has been saved in /home/user/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:F44D4dr2zoHqgj0i2iVIHQ32uk/Lx4P+raayEAQjlcs user@client
The key's randomart image is:
+--[ED25519 256]--+
|xxxx  x          |
|o.o +. .         |
| o o oo   .      |
|. E oo . o .     |
| o o. o S o      |
|... .. o o       |
|.+....+ o        |
|+.=++o.B..       |
|+..=**=o=.       |
+----[SHA256]-----+

```
Acces to sshd Config

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

```
[sshd]
enabled = true
port = ssh
#action = firewallcmd-ipset
logpath = %(sshd_log)s
maxretry = 5
bantime = 86400 
```

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

-----------------------------------------------------------

**/// BIND ///**

Install BIND

- ```sudo yum install bind bind-utils ```
- ``` sudo firewall-cmd --permanent -- add-service dns ```
- ``` sudo firewall-cmd --reload ```

Start BIND

- ``` sudo systemctl start named ```
- ``` sudo systemctl enable named ```

named.conf file for editing

- ``` sudo vi /etc/named.conf ```

named.conf.local file for editing

- ``` sudo vi /etc/named/named.conf.local ```

Run the following command to check the validity of your configuration files

- ``` sudo named-checkconf ```


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

**/// chmod & chown ///**

 - chmod = permet de modifier les permissions d’un fichier ou d’un dossier.
 - Chown = permet de changer les propriétaires d’un fichier ou d’un dossier.
 
Voici une liste des autorisations les plus courantes pour les <b> fichiers </b> :

Valeur | Valeur numérique | Explication | 
-------| --------------| ----------      | 
 rw | 600 | 	Le propriétaire peut lire et écrire. Le groupe et les autres ne peuvent rien faire avec le fichier. | 
-rw-r-r-	      | 644   | Le propriétaire peut lire et écrire, le groupe et les autres peuvent lire. |
-rw-rw-rw-	      | 666 | Le propriétaire, le groupe et les autres peuvent lire et écrire. |
-rwx–	      | 700   | Le propriétaire peut lire, écrire et exécuter. Le groupe et les autres ne peuvent rien faire avec le fichier |
 -rwxr-xr-x	 | 755 | 	Le propriétaire peut lire, écrire et exécuter. Le groupe et les’autres peuvent lire et exécuter. | 
 -rwxrwxrwx	 | 777 | 	Le propriétaire, le groupe et autres peuvent lire, écrire et exécuter. | 
 
 Les autorisations communes pour les <b> répertoires </b>:

Valeur | Valeur numérique | Explication | 
-------| --------------| ----------      | 
 drwx–	 | 700 | Seul le propriétaire peut lire et écrire dans ce répertoire. | 
drwxr-xr-x | 755  | Le propriétaire, le groupe et d’autres peuvent lire le répertoire, mais seul le propriétaire peut modifier son contenu. |

-----------------------------------------------------------

**/// nmap ///**

Scan ports

- ``` nmap -sV ip ```

-----------------------------------------------------------
-----------------------------------------------------------

**/// iSCSI ///**

Typically iSCSI is implemented in a SAN (Storage Area Network) to allow servers to access a large store of hard drive space. 

Install and configure packages (server as target)

- ``` sudo yum install -y targetcli ```
- ``` sudo systemctl start target ```
- ``` sudo systemctl enable target ```

Install and configure client (client as initiator)

- ``` sudo yum install -y iscsi-initiator-utils ```
- ``` sudo systemctl start iscsid ```
- ``` sudo systemctl enable iscsid ```
- ``` sudo systemctl start iscsi ```
- ``` sudo systemctl enable iscsi ```

Create an iSCSI backstore

- ``` sudo targetcli ```
- ``` ls ```
- ``` /backstores/fileio create file1 /tmp/disk1.img 200M write_back=false ```
- ``` ls ```

Create an iSCSI target

- ``` sudo targetcli ```
- ``` ls ```
- ``` cd /iscsi ```
- ``` create iqn.2019-06.com.localnet:filedisk1 ```

 Create an iSCSI LUN
 
 - ``` sudo targetcli ```
 - ``` cd / ```
 - ``` ls ```
 - ``` cd /iscsi/iqn.2019-06.com.localnet:filedisk1/tpg1 ```
 - ``` luns /create /backstores/fileio/filel ```
 - ``` ls ```




