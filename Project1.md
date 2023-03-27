## Documentation for Project 1
## Web stack implementation (lamp stack) - aws web console

## STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL

-- Starting by ssh into my server labelled 'Apache Web Server' from my vscode terminal in windows machine 

`sudo apt update`--(running command to update my list of packages in package manager)
![Apache-update](./Images-1/Apache-update-1a.PNG)
![Apache-update](./Images-1/Apache-update-1b.PNG) --screenshot shows update completed 

`sudo apt install apache2`--(To run apache2 package installation)
![Apache-install](./Images-1/Apache-install-2.PNG)--Screenshot of Apache2 server installation

`sudo systemctl status apache2`--(To verify that apache2 is running as a Service in our OS)
![Apache-webserver](./Images-1/Apache-webserver-3.PNG)

`curl http://localhost:80` --(using curling command with DNS Name option - to check how we can access Apache server locally within ubuntu shell. Objective - Use curl command to request our Apache HTTP Server on port 80.
![Apache-AccessServerLocal](./Images-1/Apache-AccessServerLocal-4a.PNG)
![Apache-AccessServerLocal](./Images-1/Apache-AccessServerLocal-4b.PNG)
![Apache-AccessServerLocal](./Images-1/Apache-AccessServerLocal-4c.PNG)

`http://18.207.140.84:80` --(Opened a new browser and ran command to test if we can view our Apache HTTP server via the internet. Webpage displayed validating Apache web server is operational, after installation on ubuntu system.
![Apache-AccessServerInternet](./Images-1/Apache-AccessServerInternet-5.PNG)

## STEP 2 — INSTALLING MYSQL

`sudo apt install mysql-server`--(Mysql database software installed to my apache server)
![Mysql-install](./Images-1/Mysql-install-1.PNG)

`sudo mysql` --(successful login into the MySQL console, connected as administrative database user root)
![Mysql-login](./Images-1/Mysql-Login-2.PNG)

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password>';`--(Setting up a default authenticate password for mysql,confirming mysql query for password)
![Mysql-set-password](./Images-1/Mysql-set-password-3.PNG)


`sudo mysql_secure_installation`--(running interactive security script that comes pre-installed with MySQL to secure my password, password plugin validated).
![Mysql-secure-install](./Images-1/Mysql-secure-install-4.PNG)

`mysql -u root -p`--(Test:1. successful login back to MySQL console, and 2. Insert password to gain access to mysql database service).
![Mysql-password-test](./Images-1/Mysql-password-test-5.PNG)

## STEP 3 — INSTALLING PHP

`sudo apt install php libapache2-mod-php php-mysql`--(Installing all 3 packages to PHP component;1. PHP package, 2. PHP Module, 3. Apache library).
![PHP-install-all-3-pckages-1a](./Images-1/PHP-install-all-3-pckages-1a.PNG)
![PHP-install-all-3-pckages-1b](./Images-1/PHP-install-all-3-pckages-1b.PNG)-- (PHP Installation complete)

`php -v`--(Confirming version of PHP installed).
![PHP-version](./Images-1/PHP-version-2.PNG)

## STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

`sudo mkdir /var/www/evezidomainlamp`--(Creating a domain dircetory (LAMP Stack) in my Apache HTTP server).
![VirtualHost-create-dir](./Images-1/VirtualHost-create-dir-1.PNG)

`sudo chown -R $USER:$USER /var/www/evezidomainlamp`--(Assign ownership of my new directory to my local machine as regular user).
![VirtualHost-AssignOwner-](./Images-1/VirtualHost-AssignOwner-2.PNG)

`sudo vi etc/apache2/site-available/evezidomainlamp.conf`--(crete and open a new configuration file in apache2 sites-available directory inserted script).
![VirtualHost-CreateOpen-ConfigFile](./Images-1/VirtualHost-CreateOpen-ConfigFile-3.PNG)

`sudo ls /etc/apache2/sites-available`--(Running command to test new file 'evezidomainlamp.conf' exist in sites-available directory).
![VirtualHost-Corfirm-Configfile](./Images-1/VirtualHost-Confirm-Configfile-4.PNG)

`sudo a2ensite evezidomainlamp`--(Enabling my new VirtuaHost with 'a2ensite command as Domain Name is not customised').
![VirtualHost-EnablingVH](./Images-1/VirtualHost-EnablingVH-5.PNG)

`sudo apache2ctl configtest` `sudo systemctl reload apache2` --(Testing my configuration file has no syntax error and 2. Apache webserver is reloaded and website is now active).
![VirtualHost-NoSyntaxError](./Images-1/VirtualHost-NoSyntaxError-6.PNG)

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/evezidomainlamp/index.html`--(Creating an index.html file in that location so that we can test that the virtual host works as expected - Using Public IP address)
![VirtualHost-Website-Using-PublicIPAd](./Images-1/VirtualHost-Website-Using-PublicIPAd-7.PNG)

--(Using DNS Name to launch website - achieving same result Echoing Public DNS name and Public IP address)
![VirtualHost-Website-Using-DNSName](./Images-1/VirtualHost-Website-Using-DNSName-8.PNG)

## STEP 5 — ENABLE PHP ON THE WEBSITE

 `sudo vim /etc/apache2/mods-enabled/dir.conf`--(in DirectoryIndex setting - Edit and change 'dir.conf file' order, essentially for index.php file not to be superceded by index.html file with snippit script).
![EnablePHP-changeOrder-Index](./Images-1/EnablePHP-changeOrder-Index.php-1.PNG)

`sudo systemctl reload apache2`--(Apache reloaded for changes to take effect).
![EnablePHP-ReloadApache](./Images-1/EnablePHP-ReloadApache.php-2.PNG)

`vim /var/www/evezidomainlamp/index.php`--(create a PHP test script to confirm that Apache is able to handle and process requests for PHP files).
![EnablePHP-TestScript-php](./Images-1/EnablePHP-TestScript-php-3.PNG)
![EnablePHP-Webpage](./Images-1/EnablePHP-Webpage-4.PNG)--(Webpage displaying information about the server PHP perspective).

`sudo rm /var/www/evezidomainlamp/index.php`--(Removed webpage PHP server as it contains sentive information of my PHP environment and my Ubuntu server).
![EnablePHP-Remove-Webpage](./Images-1/EnablePHP-Remove-Webpage-5.PNG)
