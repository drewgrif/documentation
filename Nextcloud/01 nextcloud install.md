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
