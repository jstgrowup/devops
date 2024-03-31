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
