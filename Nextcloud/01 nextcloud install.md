### After Debian Minimal Install

``` shell
sudo apt install -y exa micro neofetch zram-tools wget unzip curl
```

#### Change zram

```shell
 sudo micro /etc/default/zramswap
 ```
 #### Get different .bashrc
 ```shell
 rm .bashrc
 wget https://raw.githubusercontent.com/drewgrif/dotfiles/main/.bashrc
 bash
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

```shell
sudo a2ensite nextcloud.conf
```

As of Debian 12
``` shell
sudo micro /etc/php/8.2/apache2/php.ini
```

Adjust the following parameters:

* memory_limit = 512M
* upload_max_filesize = 16G
* max_execution_time = 360
* post_max_size = 16G
* date.timezone = America/New_York
* opcache.enable=1
* opcache.interned_strings_buffer=32
* opcache.max_accelerated_files=10000
* opcache.memory_consumption=128
* opcache.save_comments=1
* opcache.revalidate_freq=1

```shell
sudo systemctl restart apache2
```

## If using an external usb drive - see notes
