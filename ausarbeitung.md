# Setup Ubuntu Server

## Installation
Skip through most of the guided installation except:
 
    set language to English
 
    set keyboard layout to german
 
    set username, hostname, password
 
    tick install openSSH server
 
    install no featured server snaps
 
reboot
 
update: `sudo apt upgrade && sudo apt update`
 
reboot
 
## SSH config
edit ssh config file:
 
   `sudo vim /etc/ssh/sshd_config`
    
    Port 2222
     
    PermitRootLogin no
 
setup port forwarding to vbox:
 
    go to machine->network->advanced->port forwarding
  
    127.0.0.1:5555-> 10.0.2.15.x:2222
 
connect to guest via ssh: `ssh -p 5555 konsn@127.0.0.1`
  
### public key authentication
generate ssh key on host machine: `ssh-keygen -t rsa`
 
copy ssh key from host to guest: `scp -P 6666 ~/.ssh/id_rsa.pub konsn@127.0.0.1:/home/konsn`
 
append ssh key to authorized keys file: `cat id_rsa.pub >> .ssh/authorized_keys`
 
remove public key file: `rm id_rsa.pub`
 
disable password authentification:
 
edit ssh config file:
  
    sudo vim /etc/ssh/sshd_config`
 
        PasswordAuthentication no

## Firewall config
deny all incoming connections: `sudo ufw default deny`
 
allow ssh port: `sudo ufw allow 2222`
 
enable firewall: `sudo ufw enable
