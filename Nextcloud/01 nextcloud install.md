### After Debian Minimal Install

``` shell
sudo apt install -y exa micro neofetch zram-tools wget unzip curl
```

#### Change zram

```shell
 sudo micro /etc/default/zramswap
 ```
 
 
#### Downloading Nextcloud

```shell
wget https://download.nextcloud.com/server/releases/latest.zip
```

#### MariaDB Setup

```shell
sudo apt install -y mariadb-server
sudo mysql_secure_installation
```

#### Create Nextcloud Database

```shell
sudo mariadb
```

```shell
CREATE DATABASE nextcloud;
```
```shell
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'localhost' IDENTIFIED BY 'mypassword';
```
```shell
FLUSH PRIVILEGES;
```
CTRL+D to exit

#### Apache Webserver Setup

Installing the required packages to support Apache:

``` shell
sudo apt install php php-apcu php-bcmath php-cli php-common php-curl php-gd php-gmp php-imagick php-intl php-mbstring php-mysql php-zip php-xml
```
```shell
sudo a2enmod dir env headers mime rewrite ssl
```
```shell
sudo phpenmod bcmath gmp imagick intl
```

#### Unzip and move nextcloud

```shell
unzip latest.zip
sudo chown -R www-data:www-data nextcloud
sudo mv nextcloud.learnlinux.cloud /var/www
sudo a2dissite 000-default.conf
```
```shell
sudo micro /etc/apache2/sites-available/nextcloud.conf
```
Contents of nextcloud.conf file.
```
<VirtualHost *:80>
    DocumentRoot "/var/www/nextcloud"
    ServerName nextcloud

    <Directory "/var/www/nextcloud/">
        Options MultiViews FollowSymlinks
        AllowOverride All
        Order allow,deny
        Allow from all
   </Directory>

   TransferLog /var/log/apache2/nextcloud_access.log
   ErrorLog /var/log/apache2/nextcloud_error.log

</VirtualHost>
```