what is devops

- Requirement
  - Gathering & analysis
    - product features
    - users
    - usage
    - user requirement
    - market state
  - planning
    - estimated costs
  - Architecture design
    - roadmaps for the developers
  - development process
  - Testing and QA 
    - identify the defects to ensure the quality product is good 
  - Deployment 
    - operations 
  - Maintenance

these are known as SDLC
 there are different models in SDLC its like path to reach the same destination
 - Waterfall
   - each phase is finished before teh next phase starts
     requirement => design => development=> testing => maintenance
    - issues=> 
       - changing the requiremtns is very hard i,e going back and change something will take a long time 
 - Agile 
   - here we repeat the SDLC for smaller modules so we divide the whole project into modules and on those modules we follow the SDLC so that if there is any requiremnt change than its easier to change i,e every iteration will be discussed with tht client 
so the thing is in each of the iterations there will be so many deployement that the ops team has to do manually
along with this he has to make sure that the QA team is able to test seamlessly on the dev enviroment 


# What is continous integration
 - so when we work in a team of deveopers we put our code in version control system like github, bitbucket
 - they will pull and push code into the github 
 - it will go the build server and there it will build => test => evaluate 
 - after the build is done we create an artifact (software) its an archive of files generated from the buld process
 - based on  the language teh artifact will be packaged in different different formats for example WAR/JAR in java ZIP/TAR for other languages
 - from here it will be shipped to the servers and it will be deployed and than the testers can test the software
  Problems
 - Now lets say the developers have commited continously for 3 weeks and now the code is first sent to the build servers and it has thrown a lot of errors bugs build failures and now developers have to again rework 
 - now here the issue is that the code is merged into the repository but its not continously integrated if the integration was there it would have thrown errors during the build itself
 - the soluteion is that after every commit the code should be build and tested continously 
 - now teh issue is that developers commit a lot of times ina  day and its not humanly possible for someone to manuallly do the build and testing here comes the automation and send the notification if there is any build errrors 
 - this process of automation is known as CI continous integration
 - tools for CI => jenkins, circleci, teamcity,bamboo CI 
# what is continous delivery
- its the extension of CI 
- once everything is good the artifact is stored in the repository
- so deploment is not just shipping tgeh artifact to the server 
- it involves various steps like 
  - server provisioning 
  - dependencies installation
  - configuration changes 
  - network
  - artifact deploy 
tools: Ansible , terraform, Jenkins , octopus deploy etc 
Testings => functional, load, performance, database, network 
so now the OPS team will weite the automation code for the deployment and the testing team will write the automation code for the software testing and both will be synced with the developers source code
- so now we have integrated CI and CD process when we have a green flag from the QA team than we will deploy that to the prod
# Virtualization 
- One commputer can run different OS  
- Host OS is the laptop
- guest OS is the VM 
- VM is the virtual machine 
- snapshot 
- Hypervisor is the software that enable the making of VMs its a software by which we make virtual machines
# Hypervisor
- its a technology that allows hosting multiple virtual computers on a physical computer and the operating system that you already have installed some of the famous hypervisors are like Virtualbox from oracle
# create virtual machines
- 
# concepts
- virtual machines are completely isolated from eacxh other , so if there is any break in one of the virtual machines or someone hacks into the machine than it wont affect the main opertaing machine

# why virtual machines 
- you dont have to buy a new computer for learning a new OS
- you can test you apps or softwares on other OS as well
# types of hypervisors
  1. Type 2 : the example above is known as the type 2 hypervisors where the guest OS borrows the hardware resources from the host OS , these are for personal uses
  2. type 1; here innstead of installing an hypervisor on a host operating system we install it directly on the hardware thats why type 1 hypervisors are also known as bare metal hypervisors , so the VMs sits directly on top of the hardware
  example: Microsoft Hyper-V , vmware ESXi
  so for big servers or cloud platforms uses where we have one physical server and there will be running multiple VMs , and these VMs are completely isolated from each other 
# virtual machine sanpshot 
- all the configuration and information will be present in this file which are known as snapshots so now if there is any hardware fails than we can just take the file and run it on an another physical system having hypervisor on it 

# Vagrant 
- its a VM management tool 
- problems
  - we have to install the VMs manually
  - prone to human errors
  - if we have a huge amount of VMs than its time consuming 
Vagrant there is no OS installation in the VMs
so vagrant actually provides you something known as Images/ Box
these boxes are stored in vagrant cloud and they have  there preinstalled OS you have to download those 

- `vagrant init eurolinux-vagrant/centos-stream-9` (ie, the box name) its gonna downlaod the vagrant box from the vagrant cloud it will srtore that 
- ls (creation of the vagrant file)
- `cat Vagrantfile` 
if something is wrong you can open the file and change the config 
- `vagrant up` (if there are any errors )
- `vagrant box list` to check all the existing boxes
- `vagrant status` to check the status of the VMs
- 
