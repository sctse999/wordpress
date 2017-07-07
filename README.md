# A sendmail fixed version of official wordpress image 

### This image is derived from the official image with minimal change only to make php mail function work out of the box. Nothing more nothing less.

This image is derived from ``wordpress:4.7-php7.0``. Feel free to fork this repo and adjust the version in Dockerfile and rebuild. Happy dockering.

Sample ``docker-compose.yml``
```
version: '2'
services:
  wordpress:
    image: proactivehk/wordpress
    container_name: wordpress
    ports:
      - "80:80"
    volumes:
      - ./ssmtp.conf:/etc/ssmtp/ssmtp.conf
    restart: always
```

You need to add ``ssmtp.conf`` below for the ssmtp command line to work
```
root=postmaster

# The place where the mail goes. The actual machine name is required no 
# MX records are consulted. Commonly mailhosts are named mail.domain.com
# mailhub=mail
mailhub=yoursmtphost.com

# Where will the mail seem to come from?
#rewriteDomain=

# The full hostname
hostname=wordpress

# Are users allowed to set their own From: address?
# YES - Allow the user to specify their own From: address
# NO - Use the system generated From: address
#FromLineOverride=YES
FromLineOverride=YES
```

Note that you need to update ``hostname=wordpress`` to your wordpress hostname or otherwise it won't work

### Build this image (or your image)

```
docker build -t proactivehk/wordpress:4.7-php7.0 .
```

replace ``proactivehk`` to your username on docker hub
