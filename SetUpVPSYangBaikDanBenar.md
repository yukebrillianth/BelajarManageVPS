# Cara SetUp VPS Yang Baik dan Benar

#### 1. Add User Baru
------
```shell
sudo adduser yukebrillianth
sudo usermod -G sudo yukebrillianth
su - yukebrillianth
sudo reboot
```
#### 2. Update System
------
```shell
apt update && apt upgrade
```

#### 3. Ganti Port SSH
------
```shell
nano /etc/ssh/sshd_config
service ssh restart
```

#### 4. Install Web Server [Nginx]
------
```shell
apt -y install nginx
systemctl status nginx
```

#### 5. Install Web Server [Apache]
------
```shell
apt -y install apache2 
nano /etc/apache2/conf-enabled/security.conf

# line 25: change "ServerTokens Prod"

nano /etc/apache2/mods-enabled/dir.conf

# line 2: add file name that it can access only with directory name "DirectoryIndex index.html index.htm"

nano /etc/apache2/apache2.conf

# line 70: add to specify server name "ServerName www.srv.world"

nano /etc/apache2/sites-enabled/000-default.conf

# line 11: change to webmaster email "ServerAdmin webmaster@srv.world"

systemctl restart apache2
```

#### 6. Install SSL
------
```shell
apt -y install certbot 
certbot certonly --webroot -w /var/www/html -d srv.world 
```

#### 7. SetUp Firewall
------
```shell
ufw enable
ufw allow "Nginx Full"
ufw allow "port ssh"
Reboot
```

#### 8. Install php7.4
------
```shell
apt install software-properties-common -y
add-apt-repository ppa:ondrej/php
apt install php7.4-fpm php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-soap php7.4-zip php7.4-bcmath -y
```

#### 9. Install mysql-server
------
```shell
apt -y install mysql-server
mysql_secure_installation
```

#### Config WordPress [Vhosts]
------
(Tergantung Web Server)