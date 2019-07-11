
////configure wordpress with lamp server

Install the Apache Web Server

$ sudo apt-get install apache2

$ sudo systemctl start apache2

$ sudo systemctl enable apache2

$ sudo systemctl status apache2


////Install the MySQL Database server

The next step is to install the MySQL database server which will be used for the data storage of your WordPress site. 

$ sudo apt-get install mysql-server

Secure your MySQL server

$ sudo mysql_secure_installation

$ sudo systemctl start mysql
$ sudo systemctl enable mysql

 ////Install PHP

 The last step of our LAMP stack setup is to install PHP. WordPress is a PHP based CMS, so we need PHP for processing the dynamic content of our WordPress site.


$ sudo apt-get install php libapache2-mod-php

$ vim /var/www/html/info.php

and write on this file

        <?php
        phpinfo();
        ?>

        Finally, restart the Apache server by typing:

        $ sudo systemctl restart apache2


check php is properly config with apache server or not

localhost/info.php

////Install WordPress


move to this directory with:

$ cd /var/www/html

And download the latest WordPress installation from the official wordpress.org site with wget

$ wget -c http://wordpress.org/latest.tar.gz

Then, extract the file with:

$ tar -xzvf latest.tar.gz

We also need to set the correct permissions of this directory so our Apache web server can access these files. To give ownership of the WordPress files to our Apache web server, run the following command:

$ chown -R www-data:www-data /var/www/html/wordpress

////Create a database for WordPress

$ mysql -u root -p

To create a new database for our WordPress installation,

mysql> CREATE DATABASE wordpress_db;

mysql> GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost' IDENTIFIED BY 'PASSWORD';

mysql> FLUSH PRIVILEGES;

mysql> exit;

Make sure you are inside the /var/www/html/wordpress directory

$ mv wp-config-sample.php wp-config.php

update the database settings, replacing database_name_here, username_here and password_here

$ nano wp-config.php


--------------------------------------------------

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress_db');

/** MySQL database username */
define('DB_USER', 'wordpress_user');

/** MySQL database password */
define('DB_PASSWORD', 'PASSWORD');

/** MySQL hostname */
define('DB_HOST', 'localhost');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');
---------------------------------------------------------

Restart your Apache and MySQL server with:

systemctl restart apache2
systemctl restart mysql


run the following command to create the virtual host configuration file

$ nano /etc/apache2/sites-available/mydomain.com.conf

-----------------------------

<VirtualHost *:80>

ServerAdmin admin@mydomain.com
ServerName mydomain.com
ServerAlias www.mydomain.com
DocumentRoot /var/www/html/wordpress

ErrorLog ${APACHE_LOG_DIR}/mydomain.com_error.log
CustomLog ${APACHE_LOG_DIR}/mydomain.com_access.log combined

</VirtualHost>
--------------------------------------

 creating a symbolic link for your virtual host in /etc/apache2/sites-enabled:

 $ ln -s /etc/apache2/sites-available/mydomain.com.conf /etc/apache2/sites-enabled/

$ sudo systemctl restart apache2


and open browser localhost/wordpress open wordpress defoult page

