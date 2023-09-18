#### Using lsblk identify the intended drive to use for nextcloud

Assuming  sda

```shell
sudo apt install -y parted
```

``` shell
parted /dev/sda
```
(parted)  mklabel gpt

parted /dev/vdb mkpart primary ext4 0% 100%

