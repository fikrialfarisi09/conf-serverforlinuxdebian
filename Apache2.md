# How to install apache in debian

    root@debian:~#apt update
    root@debian:~#apt install apache2
    root@debian:~#systmctl status start
    root@debian:~#systmctl status enable
    root@debian:~#systmctl status apache
check apache2 in browser by entering ip in search

# file configuration
You can change the directory as you wish in the documentroot.
    
    root@debian:~#nano /etc/apache/sites-available/000-default.conf
