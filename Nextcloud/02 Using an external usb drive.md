#### Using lsblk identify the intended drive to use for nextcloud

Assuming  sda

```shell
sudo apt install -y parted
```

``` shell
sudo parted /dev/sda mklabel gpt

sudo parted /dev/sda mkpart primary ext4 0% 100%

Optional : parted /dev/sda name 1 my-data

sudo mkfs.ext4 /dev/sda1
```
Create a directory to mount it to (e.g. “/data”)
``` shell
sudo mkdir /data
```

Mount it using the mount command
``` shell
sudo mount /dev/sda1 /nextcloud-data
```

Add to fstab

```shell
/dev/sda1	/nextcloud-data	ext4	defaults	0	0
```

```shell
sudo chown www-data:www-data -R /nextcloud-data
sudo chmod 0750 -r /nextcloud-data
```

Once this is done.  You can use the usb drive as the data drive during installation.

