If you are already developing on Ubuntu 14.04, then it is not necessary to setup a VM to serve the qwizkool web and API. Instead, follow this
procedure to setup a Docker container.

1. Install Docker
https://docs.docker.com/engine/installation/linux/ubuntulinux/
Follow the procedure for Ubuntu 14.04

2. Get linode Docker LAMP (Linux, Apache, MySQL, PHP) stack
sudo docker pull linode/lamp

3. Run the Docker container
Please complete the [QwizkoolDeveloperSetup](QwizkoolDeveloperSetup.md) before next step

docker run -p 8080:80 -v ~/work/qwizkool/build/public_html:/var/www/example.com/public_html -t -i linode/lamp /bin/bash

This is run the docker container and log into the container. At this point,
you should see a shell prompt such as:
root@c359511b8e09:/#
Note the container id (c359511b8e09 in above example). This is needed for further
operations on the container from the host. Leave the docker shell running so that
you can configure the container when needed.

4. From the docker container shell, run the following commands:

a) Install basic components
root@c359511b8e09:/# sudo apt-get update
root@c359511b8e09:/# sudo apt-get install vim
root@c359511b8e09:/# sudo apt-get install php5-sqlite

b) Activate the mod_rewrite module 

root@c359511b8e09:/# sudo a2enmod rewrite

/etc/apache2/sites-available/example.com.conf

To use mod_rewrite from within .htaccess files (which is needed for qwizkool), edit the default VirtualHost with

sudo vi /etc/apache2/sites-available/example.com.conf
Search for “DocumentRoot /var/www/example.com/public_html” and add the following lines directly below:

<Directory "/var/www/example.com/public_html">
    AllowOverride All
</Directory>

5. Start Apache service
sudo service apache2 restart