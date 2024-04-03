Tools

- Hypervisor - Oracle VM VIrtualbox
- Automation - Vagrant
- CLI - Git bash
- IDE - Sublime Text or any text editor like notepad++

# NGnix

- For load balancing
- we will configure such that when teh request is recieved it will redirect that request to teh apache server

# Apache

- Tom Cat
- its a java web application service
- if you have a web server written in JAVA than apache its a good one
- NFS is a shared storage service
- user data will be in mysql
- the request will first go to Memcached service and that service will be connected to teh Mysql server
- [Img](https://github.com/jstgrowup/My_System_design/assets/40628582/3658511a-21a8-473c-97c5-d0ebc98cc635)

# Project setup

## Prerequisites

[docs](https://github.com/devopshydclub/vprofile-project/blob/main/vagrant/Manual_provisioning_WinMacIntel/VprofileProjectSetupWindowsAndMacIntel.pdf)

1.  Oracle VM VirtualBox
2.  Vagrant
3.  Vagrant plugins - Vagrant plugin install Vagrant-hostmanage
    `Vagrant.configure("2") do |config|
config.hostmanager.enabled = true 
config.hostmanager.manage_host = true` - plugins are known as extensions as well - when you mention the hostname and the IP address it will make sure every VM host file will be having the same hostname and IP address by default so basically it will apply these settings to all teh VMS
    there are total of 4 VMs

## vagrant-hostmanager-start

192.168.56.52 app01

192.168.56.55 db01

192.168.56.54 mc01

192.168.56.53 rmq01

192.168.56.51 web01

now we go wth the host name
here the web01 is connected to the app01 and app01 will be connected to db01 , mc01 and rmq01
here the db01 will be connected with mc01 and rmq01 and they will be connected via names

# services

we gonna setup these following services

1. Ngnix : Web service
2. Tomcat : Application server
3. RabbitMQ : Broker/Queuing Agent
4. Memcache : DB caching
5. MySql : SQL database

the idea way of setting up a stack is
Database => Cache => Queue => Appication SVC => web service
this is just a good service
all the commands
https://github.com/devopshydclub/vprofile-project/blob/main/vagrant/Manual_provisioning_WinMacIntel/VprofileProjectSetupWindowsAndMacIntel.pdf

# Database setup

1. `yum update -y` (update OS with latest packages)
2. `yum install epel-release -y` (to set the repository The command yum install epel-release -y is used in CentOS and Red Hat Enterprise Linux (RHEL) systems to install the EPEL (Extra Packages for Enterprise Linux) repository package) so that we can get access to more packages
3. `yum install git maraidb-server -y` to install mariadb package
   - MariaDB is a popular open-source relational database management system (RDBMS) that is a fork of MySQL
   - It was created by the original developers of MySQL after concerns over the acquisition of MySQL by Oracle Corporation.
   - MariaDB aims to maintain compatibility with MySQL while also adding new features and improvements
4. `systemctl start mariadb` to start the mariadb service
5. `systemctl enable mariadb` to enable it
6. `systemctl status mariadb` to check the status of the mariadb
7. ` mysql_secure_installation` this is to run mysql secure installation script
   - its gonna ask many questions and you have to answer those set the root pass to admin123
8. `mysql -u root -padmin123` now we have created the databsase server so now we are going to create a database its similar to using mongo its like starting the mongo server here we are starting the mysql database
9. `create database accounts;` to cerata a database here the database name is accounts
10. `show databases;` to see all the databases
11. ` grant all privileges on accounts.* TO 'admin'@'%' identified by 'admin123' ;` admin user should be

# Memcached server

1. `dnf intall memcached -y` (yum and dnf are both package management tools used in Linux distributions, particularly in Red Hat-based distributions like Fedora, CentOS, and RHEL. While they have similar functionalities, dnf is the newer and preferred package manager, and it eventually replaced yum in most scenarios.)
2. `systemctl start memcached` by this you can start the service and and than you can enable it
3. `systemctl enable memcached` by this you can enable the service
4. `sed -i 's/127.0.0.1/0.0.0.0/g'/etc/sysconfig/memcached` search and replace the local IP to 0.0.0.0 so some service only search for the local service all the IPs are open
5. `vim /etc/sysconfig/memcached` to check tehe file
6. `sudo systemctl restart memcached` to restart the memcached service
7. `logout`

# Rabbit MQ

1. `yum update -y` its gonna update the OS
2. `yum install epel-release -y` update teh epel repository
3. `dnf -y install centos-release-rabbitmq-38` to install the rabbitmq for centos
4. `dnf --enablerepo=centos-rabbitmq-38 -y install rabbitmq-server` enable the repository and install the rabbitmq server
5. `systemctl start rabbitmq-server` to start the server
6. `systemctl enable rabbitmq-server` to enable the server
7. `sh -c ' echo "[{rabbit,[{loopback_users,[]}]}]." > /etc/rabbitmq/rabbitmq.config'`
8. `rabbitmqctl add_user test test` add user test user with pass test
9. `rabbitmqctl set_user_tags test administrator` for this test user we gonna set a tag called administrator this will be used by our vprofile application to connect to our vprofile application
10. `systemctl restart rabbitmq-server` restart the service and check the status
11. `systemctl status rabbitmq-server` to check the status of the server because we have made the configuration in the server so thats why we check the status

# Tomcat

1. `yum update -y` to update the OS
2. `yum install epel-release -y` enable the epel repository (yum: yum is a command-line package manager used in some Linux distributions, particularly in CentOS, RHEL, and other RPM-based distributions. It helps you install, update, and manage software packages on your system.

install: This is an action that tells yum to install a package.

epel-release: This is the name of the package that yum will install. In this case, it's the "Extra Packages for Enterprise Linux (EPEL)" repository configuration package. EPEL provides additional software packages not included in the standard CentOS/RHEL repositories.)

3. `dnf -y install java-11-openjdk java-11-openjdk-devel` to install open jdk 11 for java 11 jdk and jre are different jre is java runtime enviroment and jdk is java development kit 4. `dnf install git maven wget -y` maven idk man

4. `wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.75/bin/apache-tomcat-9.0.75.tar.gz` download the apache server

5. `tar xzvf apache-tomcat-9.0.75.tar.gz` from the above command its gonna downlaod a zip folder called apache-tomcat and now you can extract the the folder using this command - tar is a command-line utility used in Unix-like operating systems to package files and directories into an archive file (also known as a "tarball") and to extract files from an archive -

- x: This option tells tar to extract files from the archive.
- z: This option tells tar to use gzip compression/decompression when working with the archive. It indicates that the archive file is compressed using gzip.
- v: This option stands for "verbose." It tells tar to print the names of the files it's extracting as it goes.
- f: This option is used to specify the filename of the archive to work with. The filename immediately follows this option.
  APACHE is the org name and tomcat is the name of the service and server

6. `useradd --home-dir /usr/local/tomcat --shell /sbin/nologin tomcat` add a tomcat user
7. `cp -r apache-tomcat-9.0.75/* /usr/local/tomcat` to move everything from apache-tomcat-9.0.75 to the usr folder
8. `chow -R tomcat.tomcat /usr/local/tomcat`
9. `vi /etc/systemd/system/tomcat.service` to open a file
10. `[Unit]
Description=Tomcat
After=network.target
[Service]
User=tomcat
WorkingDirectory=/usr/local/tomcat
Environment=JRE_HOME=/usr/lib/jvm/jre
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/usr/local/tomcat
Environment=CATALINE_BASE=/usr/local/tomcat
ExecStart=/usr/local/tomcat/bin/catalina.sh run
ExecStop=/usr/local/tomcat/bin/shutdown.sh
SyslogIdentifier=tomcat-%i
[Install]
WantedBy=multi-user.target` paste this and press esc and do :wq to save and exit
11. `systemctl daemon-reload` so this to reload the tomcat server
    - When you make changes to systemd configuration files, such as unit files (.service, .socket, .target, etc.), you need to inform systemd to reload these changes. This is where systemctl daemon-reload comes into play
12. `systemctl start tomcat` to start the service
13. `systemctl enable tomcat` to enble the service
14. ` git clone -b main https://github.com/hkhcoder/vprofile-project` clone the project
15. `cd vprofile-project/`
16. ` vim src/main/resources/application.properties` see the file there are configurations
17. `mvn install` its gonna downllad the artifact its like the deployable application.
18. `ls target` here you will find the folder called vprofile v2.war and this is the artifact its like a zip form of vprofile-v2.
19. `systemctl stop tomcat` stop the server.
20. `ls /usr/local/tomcat/webapps` here you will get the folder called ROOT.
21. `rm -rf /usr/local/tomcat/webapps/ROOT` its gonna remove the ROOT folder.
22. `cp target/vprofile-v2.war  /usr/local/tomcat/webapps/ROOT.war` copy the war folder and make a root folder.
23. `ls /usr/local/tomcat/webapps/` you will see the ROOT folder and now you have successfully deleted the default root folder and instal;led the artifact as the default root folder.
24. `systemctl start tomcat` start the tomcat server and now if you do the ls on `/usr/local/tomcat/webapps/` you will observe that there is a ROOT folder so what happens is the service has extracted the ROOT.war and it has created a ROOT folder now that becomes our default application.
25. `systemctl status tomcat` to check the status of the service if its running or not.

# NGINX setup

1. `apt update` to find the latest packages
2. `apt upgrade` to upgrade the latest packages
3. `apt install ngnix -y` to install the ngnix
4. ` vi /etc/ngnix/sites-available/vproapp` make a file and put my custom configuration
5. `upstream vproapp {
server app01:8080;
}
server {
listen 80;
location / {
proxy_pass http://vproapp;
}
}` this is the configuration
6. `ls /etc/nginx/sites-available/` this is where will be having our configuration
7. `ls /etc/ngnix/sites-enabled` here will be having a link
8. `ls -l /etc/nginx/sites-enabled/` you will see `lrwxrwxrwx 1 root root 34 Apr  1 18:18 default -> /etc/nginx/sites-available/default` this is a link now from enabled we have to create a link to our nginx server
9. `rm -rf /etc/nginx/sites-enabled/default` this will remove the link
10. `ln -s /etc/nginx/sites-available/vproapp /etc/nginx/sites-enabled/vproapp` ln -s will create a link to our nginx server
11. now if you do `ls -l /etc/nginx/sites-enabled/` you will see `lrwxrwxrwx 1 root root 34 Apr  1 18:35 vproapp -> /etc/nginx/sites-available/vproapp`
12. `systemctl restart nginx` restart the service
13. `systemctl status nginx`

# Flow Of Execution

1. Setup tools mentioned in prerequisite video
2. clone source code
3. cd into the vagrant dir
4. validate
5. setup all the services
   - Mysql
   - Memcached
   - Rabbit MQ
   - tomcat
6. login to web01
7. `ip addr show` to get the IP address
8. `vagrant destroy --force` to destroy all the VMs

# Setup for automatically

1. `cd Automated_provisioning_WinMacIntel/`
2. `vagrant up` and it will execute all the commands and it will
