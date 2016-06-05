Serving directory
/var/www/example.com/public_html/


sudo apt-get update
sudo apt-get install vim
sudo apt-get install php5-sqlite


Activate the mod_rewrite module with

sudo a2enmod rewrite/etc/apache2/sites-available/example.com.conf

To use mod_rewrite from within .htaccess files (which is needed for qwizkool), edit the default VirtualHost with

sudo vi /etc/apache2/sites-available/example.com.conf
Search for “DocumentRoot /var/www/example.com/public_html” and add the following lines directly below:

<Directory "/var/www/example.com/public_html">
    AllowOverride All
</Directory>

sudo service apache2 restart