# LinuxCommands Ubuntu - Debian
in progress


- sudo apt-get update
- sudo apt-get upgrade
- sudo apt dist-upgrade

**/// htop ///**

> Display running processes, kill them, and change their priority level. 

- sudo apt-get install htop

**/// SSH ///**

> Install

- sudo apt-get update
- sudo apt-get install openssh-server
- ssh-keygen -t ed25519

> UFW

- sudo ufw enable
- sudo ufw status
- sudo ufw status verbose

> Deny all outgoing traffic (paranoid)
- sudo ufw default deny outgoing comment 'deny all outgoing traffic'

> allow ssh
- sudo ufw limit in ssh comment 'allow SSH connections in'
 
> allow traffic out on port 53 -- DNS
- sudo ufw allow out 53 comment 'allow DNS calls out'

> allow traffic out on port 123 -- NTP
- sudo ufw allow out 123 comment 'allow NTP out'

> allow traffic out for HTTP, HTTPS, or FTP
  apt might needs these depending on which sources you're using
- sudo ufw allow out http comment 'allow HTTP traffic out'
- sudo ufw allow out https comment 'allow HTTPS traffic out'
- sudo ufw allow out ftp comment 'allow FTP traffic out'

> allow whois
- sudo ufw allow out whois comment 'allow whois'

> allow traffic out on port 68 -- the DHCP client
  you only need this if you're using DHCP
- sudo ufw allow out 68 comment 'allow the DHCP client to update'

-----------------------------------------------------------

**/// neofetch ///**

- sudo apt install neofetch
- cat /proc/version

-----------------------------------------------------------


**/// How can I install Split Terminator - Multitasking ///**

> Terminator

- sudo apt-get install terminator

-----------------------------------------------------------


**/// How can I install Midnight Commander  ///**

> MC - You need to enable the universe repository:

- sudo add-apt-repository universe

- sudo apt update

- sudo apt install mc

-----------------------------------------------------------

**/// Timeshift Linux ///**

https://www.tecrobust.com/install-timeshift-linux-and-create-backup/
