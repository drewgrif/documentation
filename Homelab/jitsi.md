# Jitsi installation on Linode

## Domain Setup
Currently using linode dedicated 4 core 8 G RAM - static ip and RDNS
* Make sure your using linode dns

# Retrieve the latest package versions across all repositories

```
sudo apt update
sudo apt install apt-transport-https
```


Make sure:
```
sudo apt-add-repository universe (likely already installed)
```

```
sudo hostnamectl set-hostname jitsi.sample.com
```

```
sudo nano /etc/hosts
```

After making sure linode is using a static ip address, add the static ip into the /etc/hosts file

127.0.0.1
x.x.x.x jitsi.sample.com


## Configure Firewall
```
sudo ufw allow OpenSSH
```

```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow 3478/udp
sudo ufw allow 5349/tcp
sudo ufw allow 10000/udp
```

```
sudo ufw status
```

If not enable, enable it.

## Installing jitsi

Add Prosody
```
sudo curl -sL https://prosody.im/files/prosody-debian-packages.key -o /etc/apt/keyrings/prosody-debian-packages.key
echo "deb [signed-by=/etc/apt/keyrings/prosody-debian-packages.key] http://packages.prosody.im/debian $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/prosody-debian-packages.list
sudo apt install lua5.2
```

Add Jitsi

```
curl -sL https://download.jitsi.org/jitsi-key.gpg.key | sudo sh -c 'gpg --dearmor > /usr/share/keyrings/jitsi-keyring.gpg'
echo "deb [signed-by=/usr/share/keyrings/jitsi-keyring.gpg] https://download.jitsi.org stable/" | sudo tee /etc/apt/sources.list.d/jitsi-stable.list
```

```
rm jitsi-key.gpg.key prosody-debian-packages.key
sudo apt update
sudo apt install jitsi-meet
```

Use CORRECT Hostname
Use Let's Encrypt for SSL

## Securing Room Creation
Prosody configuration

If you have installed Jitsi Meet from the Debian package, these changes should be made in /etc/prosody/conf.avail/[your-hostname].cfg.lua
Enable authentication

Inside the VirtualHost "[your-hostname]" block, replace anonymous authentication with hashed password authentication:
```
VirtualHost "jitsi-meet.example.com"
    authentication = "internal_hashed"
```
Replace jitsi-meet.example.com with your hostname.

Also, add to the botttom of this file

```
VirtualHost "guest.jitsi.your_domain"
    authentication = "anonymous"
    c2s_require_encryption = false
    modules_enabled = {
            "bosh";
            "ping";
            "pubsub";
            "speakerstats";
            "turncredentials";
            "conference_duration";
    }
```

Next, open another configuration file at /etc/jitsi/meet/jitsi.your_domain-config.js with a text editor:
```
    sudo nano /etc/jitsi/meet/jitsi.your_domain-config.js
```
Use the search tool CTRL+W again to search for anonymousdomain:, which will take you to the following line:
/etc/jitsi/meet/your_domain-config.js
```
        // anonymousdomain: 'guest.example.com',
```
Edit this line to look like the following by removing the double slashes // at the start of the line:
/etc/jitsi/meet/your_domain-config.js
```
        anonymousdomain: 'guest.jitsi.your_domain',
```
You will use the guest.jitsi.your_domain hostname that you used previously. This configuration tells Jitsi Meet what internal hostname to use for the un-authenticated guests. Save and close the file.
