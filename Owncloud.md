# How to install Owncloud Server
First we start 

root@debian:~#apt update

root@debian:~#apt install -y software-properties-common ca-certificates lsb-release apt-transport-https

root@debian:~#mkdir -p /etc/apt/keyrings

root@debian:~#curl -fsSL https://packages.sury.org/php/apt.gpg | tee /etc/apt/keyrings/sury-php.gpg > /dev/null 

root@debian:~#echo "deb [signed-by=/etc/apt/keyrings/sury-php.gpg] https://packages.sury.org/php $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/sury-php.list

root@debian:~#apt update

# Install php7.4 dan mariadb

root@debian:~#apt install php7.4 php7.4-{opcache,gd,curl,mysqlnd,intl,json,ldap,mbstring,mysqlnd,xml,zip}

root@debian:~#apt install mariadb-server

root@debian:~#mysql_secure_installation

Enter current password for root (enter for none):

Set root password? [Y/n] Y

New password:

Re-enter new password:

Remove anonymous users? [Y/n] Y

Disallow root login remotely? [Y/n] Y

Remove test database and access to it? [Y/n] Y

Reload privilege tables now? [Y/n] Y

root@debian:~#mysql -u root -p

enter the username and password

MariaDB [(none)]> CREATE DATABASE owncloud;

MariaDB [(none)]> GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost' IDENTIFIED BY 'Pass123';

MariaDB [(none)]> FLUSH PRIVILEGES;

MariaDB [(none)]> EXIT;

root@debian:~#unzip /home/ukk/owncloud-complete-latest.zip -d /var/www/html/

Adjust the name "name" here according to the FTP username when logging in

Changing ownCloud access rights

root@debian:~#chown -R www-data:www-data /var/www/html/owncloud/

Copy file sites-available

root@debian:~#cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/owncloud.conf

root@debian:~#nano /etc/apache2/sites-available/owncloud.conf

In this file, just add owncloud to the DocumentRoot line to make it
DocumentRoot /var/www/html/owncloud

root@debian:~#a2dissite 000-default.conf

root@debian:~#a2ensite owncloud.conf

root@debian:~#systemctl restart apache2

CONTINUE OWNCLOUD CONFIGURATION IN BROWSER
