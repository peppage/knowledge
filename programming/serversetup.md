# Basic server setup

What I do when I want to setup a server for side projects. You should keep in mind security is light
and it will not contain anything sensitive. I picked up a lot from
[this guide](https://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers).

### Install/update

    apt-get update
    apt-get upgrade
    apt-get install fail2ban
    apt-get install nginx htop tmux postgresql
    
### Block root login

I'm not going to block by IP because there are several IPs I need to login
from. Again, this isn't a secure app server. Changing these values will not
automatically boot your session.
    
    vim /etc/ssh/sshd_config
    
Change these two lines,

    PermitRootLogin no
    PasswordAuthentication no
    
### Create user

In this step you handle adding the `authorized_keys` file yourself.

    adduser mca
    mkdir /home/mca/.ssh
    chmod 700 /home/mca/.ssh
    chown mca:mca /home/mca -R
    visudo
    
Give mca sudo access,

    mca ALL=(ALL:ALL) ALL

### Firewall

Be aware this may boot you from 

    ufw allow 80
    ufw allow 443
    ufw allow 20
    ufw enable
    
### Auto updates

    apt-get install unattended-upgrades
    
Edit this file `vim /etc/apt/apt.conf.d/10periodic`,

    APT::Periodic::Update-Package-Lists "1";
    APT::Periodic::Download-Upgradeable-Packages "1";
    APT::Periodic::AutocleanInterval "7";
    APT::Periodic::Unattended-Upgrade "1";
   
### Postgres 

    su postgres
    createuser mca
    vi /etc/postgresql/VER/main/pg_hba.conf
    
Edit the file to allow for all local connections. Changing it to "trust".

    host all all 127.0.0.1/32 trust
    
Then restart the service

    service postgresql restart
    
