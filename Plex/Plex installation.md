**Assuming you are starting with headless Debian Server
#### OPTIONAL - Get different .bashrc
 ```shell
 rm .bashrc
 wget https://raw.githubusercontent.com/drewgrif/dotfiles/main/.bashrc
 bash
 ```
 
#### Requirements
```shell
sudo apt install apt-transport-https curl wget sudo gnupg2 -y
```

```shell
echo "deb https://downloads.plex.tv/repo/deb public main" | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
```

```shell
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
```

```shell
sudo apt update
```

When you update, you will likely get an # [apt-key deprecation warning when updating system](https://askubuntu.com/questions/1398344/apt-key-deprecation-warning-when-updating-system)

```shell
cd /etc/apt
sudo cp trusted.gpg trusted.gpg.d
```

Test again (deprecation warning should gone)
```shell
sudo apt update
```

```shell
sudo apt install plexmediaserver
```

If your using my [.bashrc script](https://raw.githubusercontent.com/drewgrif/dotfiles/main/.bashrc), you can use the following command:

```shell
myip
```

####  Goto http://myinternal_ip:32400/web
