# PROJECT 1 - INSTALLING APACHE AND UPDATING THE FIREWALL
`sudo apt update`
![sudo apt update command](./images/sudo-apt-update.JPG)
`sudo apt install apache2`
![sudo apt install apache2](./images/sudo-apt-install-apache2.JPG)
`sudo systemctl status apache2`
![sudo systemctl status apache2](./images/sudo-systemctl-status-apache2.JPG)

## Add a rule to EC2 configuration to open inbound connection through port 80
![Edit EC2 Security Group Setting](./images/open-http-port80.JPG)
## Test to see if webserver responds to curl command
`curl http://localhost:80`
![curl http://localhost:80](./images/curl-webserver.JPG)
## Test on browser to see webserver responds
![Browser test using public IP](./images/webserver-default-page.JPG)

# PROJECT 1 - INSTALLING MYSQL
`sudo apt install mysql-server`
![sudo apt install mysql-server](./images/sudo-apt-install-mysql-server.JPG)
## Connect to mysql and secure root user password
`sudo mysql`
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
![SQL statement to secure mysql root user](./images/secure-mysql-root-user.JPG)

# PROJECT 1 - INSTALLING PHP
`sudo apt install php libapache2-mod-php php-mysql`
![sudo apt instll php](./images/sudo-apt-install-php.JPG)

# PROJECT 1 - CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
`sudo mkdir /var/www/projectlamp`
`sudo chown -R $USER:$USER /var/www/projectlamp`
`sudo vi /etc/apache2/sites-available/projectlamp.conf`
![projectlamp.conf file](./images/vhost-config.JPG)
## Enable new virtual host and disable default apache website
`sudo a2ensite projectlamp`
`sudo a2dissite 000-default`
`sudo apache2ctl configtest`
## Reload Apache webserver for changes to take effect
`sudo systemctl reload apache2`
`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
![Test the new virtual host on a browser](./images/new-vhost-html-test.JPG)

# PROJECT 1 - ENABLE PHP ON THE WEBSITE
`sudo vim /etc/apache2/mods-enabled/dir.conf`
![Modify dir.conf to make php default](./images/modify-dir-conf.JPG)
`sudo systemctl reload apache2`
## Create a new index.php file in the virtual directory
`vim /var/www/projectlamp/index.php`
` <?php phpinfo(); ` 
![Output of php file on a Web Browser](./images/php-test-output.JPG)
## Remove php test page because of sensitive information
`sudo rm /var/www/projectlamp/index.php`

# END OF PROJECT 1
