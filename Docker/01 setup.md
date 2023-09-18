## Installing Docker

Install dependencies:

```shell
sudo apt -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

Then, add the Docker repository key:

```shell
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Afterwards, add the Docker APT repository. Make sure to replace amd64 with arm64 if you're running this on an ARM-based CPU.

``` shell
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

Finally, install Docker and docker-compose with the following commands:

```shell
sudo apt update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose
```

If you're running as a non-root user, you might need to add your user to the docker group using the following command:

```shell
sudo usermod -aG docker username
```

Then, log out and then log back in again for the changes take effect.


PORTAINER
=========
```shell 
docker volume create portainer_data
```
```shell
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

localhost:9443