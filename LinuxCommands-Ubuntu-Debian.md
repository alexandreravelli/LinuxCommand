# LinuxCommands RHEL - Ubuntu - Debian
in progress


- sudo apt-get update
- sudo apt-get upgrade

**/// htop ///**

> Display running processes, kill them, and change their priority level. 

- sudo apt-get install htop

**/// SSH ///**

> Install

- sudo apt-get update
- sudo apt-get install openssh-server
- ssh-keygen -t ed25519

> UFW

- sudo ufw allow ssh

> On boot

- sudo systemctl enable ssh

-----------------------------------------------------------

**/// How can I install Split Terminator - Multitasking ///**

> Terminator

- apt-get install terminator

-----------------------------------------------------------


**/// How can I install Midnight Commander  ///**

> MC - You need to enable the universe repository:

- sudo add-apt-repository universe

- sudo apt update

- sudo apt install mc

-----------------------------------------------------------
