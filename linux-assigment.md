/////////////////////

Install and configure apache/httpd

solution step-

$ sudo apt-get update  //this cmd to install latest update

$ sudo apt install apache2 //install apache server

$ apache2 -version  //check apache install or not

then configure the firewall setting

$ sudo ufw app list  //List the UFW application profiles

$ sudo ufw allow 'Apache'  //Allow Apache on UFW and verify its status

$ sudo systemctl status apache2  //check apache services run properly

$ hostname -I //check host ip and check apache is running



//////////////

Install and configure nginx - configure it to run as reverse proxy to apache

solution step-

$sudo apt-get install nginx  //install nginx server

configure the nginx

$sudo nano /etc/nginx/sites-available/example   //Open up the nginx configuration.


set you up to use nginx as the front end server

server {
        listen   80; 

        root /var/www/; 
        index index.html index.htm;

        server_name example.com; 

        location / {
        try_files $uri $uri/ /index.php;
        }

        location ~ \.php$ {
        
        proxy_set_header X-Real-IP  $remote_addr;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header Host $host;
        proxy_pass http://127.0.0.1:8080;

         }

         location ~ /\.ht {
                deny all;
        }
}

--------------------------------------------------------------------------------

Activate the virtual host.

$ sudo ln -s /etc/nginx/sites-available/example /etc/nginx/sites-enabled/example

//Additionally, delete the default nginx server block.

$ sudo rm /etc/nginx/sites-enabled/default

// Install Apache

$ sudo apt-get install apache2

//Configure Apache

$ sudo nano /etc/apache2/ports.conf











////////////

Install and configure 'ntp' - with singapore time zone

$ sudo apt-get update


$sudo apt-get install ntp

$ timedatectl list-timezones  //list available time zone

$ timedatectl set-timezones desired_timezone  //set timezone


For example, to set the timezone Singapore use this command:

sudo timedatectl set-timezone Asia/Singapore

$ timedatectl  //Verify that the timezone has been set properly



/////////////

Install Tomcat version 8 (a brief explaination about the it's directories in doc)

$ sudo apt-get update

$ sudo apt-get install defoult-jdk  // install java jdk

 Create Tomcat User

 $ sudo groupadd tomcat  //For security purposes, Tomcat should be run as an unprivileged user

 $ sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat  //create a new tomcat user. We'll make this user a member of the tomcat group, with a home directory of /opt/tomcat (where we will install Tomcat), and with a shell of /bin/false (so nobody can log into the account):

 install tomcat

 $ curl -O http://apache.mirrors.ionfish.org/tomcat/tomcat-8/v8.5.5/bin/apache-tomcat-8.5.5.tar.gz  //download the link that you copied from the Tomcat website

  install Tomcat to the /opt/tomcat directory.

  $ sudo mkdir /opt/tomcat //make directorie in /opt

  $ sudo cp -r apache-tomcat-8.5.42/* /opt/tomcat/  //copy unzip file to /opt/tomcat folder


  Update Permissions

  $ cd /opt/tomcat //change the directory where copy tomcat file

  $ sudo chgrp -R tomcat /opt/tomcat // Give the tomcat group ownership over the entire installation directory

  give the tomcat group read access to the conf directory and all of its contents, and execute access to the directory itself
                                        
  $ sudo chmod -R g+r conf
  $ sudo chmod g+x conf

  Make the tomcat user the owner of the webapps, work, temp, and logs directories

  $ sudo chown -R tomcat webapps/ work/ temp/ logs/

  Create a systemd Service File

  $ sudo update-java-alternatives -l  // to know path where Java is installed

  we can create the systemd service file. Open a file called tomcat.service in the /etc/systemd/system 

  $ sudo nano /etc/systemd/system/tomcat.service

 ----past following content in tomcat .service file

  [Unit]
        Description=Apache Tomcat Web Application Container
        After=network.target

        [Service]
        Type=forking

        Environment=JAVA_HOME=/usr/lib/jvm/java-8-oracle/jre
        Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
        Environment=CATALINA_HOME=/opt/tomcat
        Environment=CATALINA_BASE=/opt/tomcat
        Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
        Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

        ExecStart=/opt/tomcat/bin/startup.sh
        ExecStop=/opt/tomcat/bin/shutdown.sh

        User=tomcat
        Group=tomcat
        UMask=0007
        RestartSec=10
        Restart=always

[Install]
WantedBy=multi-user.target
-----------------------------------------------------------------------------------------------------------------

$ sudo systemctl daemon-reload  //know about our service file

$ sudo systemctl start //start tomcat server

$ sudo systemctl status  // know status of tomcat server

$ sudo ufw allow 8080  //Tomcat uses port 8080 to accept conventional requests. Allow traffic to that port by typing


/////////////


Install java version 8 with home directory set as an environment variable

$ sudo apt install openjdk-8-jdk //to install java version 8

$ export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64   //set java home path

$ echo $JAVA_HOME //to know java path successfully saved or not

   Add JAVA bin directory to the PATH variable

  $ export PATH=$PATH:$JAVA_HOME/bin


  $ echo $PATH  //check the path

  $ java -version  //test java setup


///////////////////////

Install 'build essentials' 

$ sudo apt-get install build-essential


///////////////////////
