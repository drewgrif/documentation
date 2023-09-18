## Nextcloud YAML 
I am using a premounted EXTERNAL USB Drive for DATA

```YAML
version: '2'

services:
  db:
    image: mariadb
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - /home/drew/usb/nextcloud/db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=Bund7zXeVz7YnFknLGcnUjHtk #CHANGE THIS
      - MYSQL_PASSWORD=HFdMe9rn5kf7A8Pqc8v86Pre5 #CHANGE THIS
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 8088:80
    links:
      - db
    depends_on:
      - db
    volumes:
      - /home/drew/usb/nextcloud/nextcloud:/var/www/html
      - /home/drew/usb/nextcloud/app/config:/var/www/html/config
      - /home/drew/usb/nextcloud/app/custom_apps:/var/www/html/custom_apps
      - /home/drew/usb/nextcloud/app/data:/var/www/html/data
      - /home/drew/usb/nextcloud/app/themes:/var/www/html/themes/
      - /etc/localtime:/etc/localtime:ro
    environment:
      - MYSQL_PASSWORD=HFdMe9rn5kf7A8Pqc8v86Pre5  #CHANGE THIS TO MATCH THE MYSQL_PASSWORD ABOVE
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```
