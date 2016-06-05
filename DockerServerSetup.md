If you are already developing on Ubuntu 14.04, then it is not necessary to setup a VM to serve the qwizkool web and API. Instead, follow this
procedure to setup a Docker container.  

1. Install Docker  
https://docs.docker.com/engine/installation/linux/ubuntulinux/  
Follow the procedure for Ubuntu 14.04  

2. Get linode Docker LAMP (Linux, Apache, MySQL, PHP) stack  
`sudo docker pull linode/lamp`

3. Run the Docker container  
Please complete the [QwizkoolDeveloperSetup](QwizkoolDeveloperSetup.md) before next step  
`mkdir -p ~/work/qwizkool/database`
`chmod 777 -R ~/work/qwizkool/database`
`docker run -p 8080:80 -v ~/work/qwizkool/build/public_html:/var/www/example.com/public_html -v ~/work/qwizkool/database:/var/www/example.com/database -t -i linode/lamp /bin/bash`  

This is run the docker container and log into the container. At this point, you should see a shell prompt such as:
`root@c359511b8e09:/#`  
Note the container id (c359511b8e09 in above example). This is needed for further
operations on the container from the host. Leave the docker shell running so that
you can configure the container when needed.  

The above command makes the qwizkool server available to the host on port 8080. So you would browse to localhost:8080 from host
browser to launch qwizkool web. In addition, the command mounts the build directory of the development environment so that the latest
build is always hosted in real time.  

4. From the docker container shell, run the following commands:  

* Install basic components  
`root@c359511b8e09:/# sudo apt-get update`  
`root@c359511b8e09:/# sudo apt-get install vim`  
`root@c359511b8e09:/# sudo apt-get install php5-sqlite`  

* Activate the mod_rewrite module  

`root@c359511b8e09:/# sudo a2enmod rewrite`  

To use mod_rewrite from within .htaccess files (which is needed for qwizkool), edit the default VirtualHost with  

`sudo vi /etc/apache2/sites-available/example.com.conf`
Search for `DocumentRoot /var/www/example.com/public_html` and add the following lines directly below:  

```
<Directory "/var/www/example.com/public_html">
    AllowOverride All
</Directory>
```
5. Create the database folder  
`root@c359511b8e09:/# mkdir -p /var/www/example.com/database`  
`root@c359511b8e09:/# sudo chmod 777 -R /var/www/example.com/database`  
The qwizkool database file qwizkool.db will get created here.  

6. Start Apache service  
```
root@c359511b8e09:/# vi /root/.bashrc
Add this line the the end : service apache2 restart
Save the file
root@c359511b8e09:/# sudo service apache2 restart
```
7. From the host system, launch the browser and go to http://localhost:8080/
You should see the qwizkool home page. Enable the developer pane on the browser and watch the Network tab. 
Click on "Explore" button in qwizkool home page. If you do not see eny errors, then the server setup is complete.  

8. Changes done to the Docker container are not persistent. These changes need to be committed so that you get the fully configured
container next time you launch docker. The procedure is as follows:  

From another host shell:  
`docker commit -m "Qwizkool" -a "qwizkool" c359511b8e09 qwizkool/server`  

Remember to replace the docker id `c359511b8e09` with yours.  

Once the command completes, exit the container  

`root@c359511b8e09:/# exit  

Now launch the new container and make sure all changes are persisted and the the server works as expected.  
`docker run -p 8080:80 -v ~/work/qwizkool/build/public_html:/var/www/example.com/public_html -v ~/work/qwizkool/database:/var/www/example.com/database -t -i qwizkool/server /bin/bash`  



