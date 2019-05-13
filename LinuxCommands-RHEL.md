# LinuxCommands RHEL
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

- ssh-keygen -t ed25519

-----------------------------------------------------------

**/// PWD ///**

-----------------------------------------------------------

pwd

-----------------------------------------------------------

**/// Touch ///**

-----------------------------------------------------------

touch fichier.txt

-----------------------------------------------------------

**/// VI ///**

-----------------------------------------------------------

vi fichier.txt (e pour edit)

-----------------------------------------------------------

uname -a / df -ah 
