# Linux

- Linux is an open source kernal

## Principles

- Everything os a file (including hardware)
- small single purpose programs
- Ability to chain programs together for comples operations
- Avoid captive User Interface
- configuration data stored

## why linux

- opencource
- community support
- support wide variety of hardware
- customization
- automation
- security

## Architecture

hardware=> linux kernal => shell => commands(cd,ls,mkdir)

## linux didstros

- Ubuntu Linux
- Linux Mint
- Debian
- OpenSuse
- Arch Linux

## Popular server linux OS

- Red hat enterprise Linux
- Ubuntu server
- Centos
- SUSE Enterprise

## Most used linux distros currently in IT industry

- RPM based : RHEL,Centos, Oracle Linux , amazon linux
- Debian based : ubuntu server, Kali Linux 
difference is the packaging system in these both 
# Commands
![commands](https://github.com/jstgrowup/My_System_design/files/14549348/LinuxQuickstartV5.pdf)
1. `touch` to create a a file
2. `mkdir` to create a folder
3. `cp {fileName} destination` exaple cp dockerfile.txt dev/ this command is to copy and paste a file you can give absolute path
4. `cp -r {dir name} {destination dir name}` if you want to copy and paste directories than you have to use this command
5. `mv {file name} {directory name}` if you want to move a file to a a directory than you cna use mv command 
6. `mv {previous file name} {new file name}` you can also use mv to rename the file
7. `mv *.txt textdir/` this * means everything so here i am trying to move all teh files ending with .txt to textdir
8. `rm {filename}` if you want to deleete a file than you can use rm
9. `rm -r {dirname}` if you want to remove a directory than you have to use -r 
10. `sudo yum install vim -y` by this command you can install vim which is a text editor 
11. `vim {file name}` it will create a file 
     - use `i` to insert
     - use `:wq!` to save and exit fromt the vim file , ! is for forcefull
     - if you wannna edit the file please repeat the same command as the creation
     - `cat {filename}` to open the file and whats written inside the file
     - `:se nu` it will show you the line numbers as well
     - `shift + g` last line of the file
     - `gg` will take you to the first line of the 
     - `y` for copying a line and for pasting use `p`
     - `dd` for deleting a line as well as cut a line
12. # Types of files in Linux
    `file {file name}` it will return you the type of the file 
    
13. # Filter and IO redirection
     - `grep {target term} {file name}` lets say you wnat to search a word in a file than you can use this command
     - linux is case sensitive so if you fin for a word example firewall itsd gonna give you the exact results for this you can use `grep -i {target word} {file name}`
     - `grep -i {target word} *` lets say i want to find a word in all the files in the current directory
     - `grep -R {target word} /etc/*` its gonna fing the target word in the entire etc directory 
     - `grep -vi {target word} {file name}` its gonna give you all teh words other than the target word its kin of a reverse search
     - `less {filename}` its gonna show you the contents of the file and you can use teh up arrow and down arrow to go through the coontents and use `q` to quit and exit 
     - `head {file name}` to see first 10 lines of teh file 
     - `head -{number of lines} {file name}` to the first number of lines that are defined in teh number of lines
     - `tail -f {file name}` this gonna show you the last 10 lines and if there is any change in teh file its gonna show you , its helps in troubleshooting as well
 14. # input/output redirection (>>)
 redirection is a process where we can copy the output of any  commands,files into a new file
     - `{output 1}>{target file path}` here its a single > so its gonna replace everythign that is already present in that file with the new output example : `date>/tmp/sysinfo.txt`,`free -m > /dev/null`
     - `{output 1}>>{target file path}` here its a double > so its gonna append everything that is already present in that file with the new output example : `date>>/tmp/sysinfo.txt`
     - `{the command} &>> /tmp//error.log` here i am telling please redirect the errors or anything that comes to the temp error file
    ## Piping
    - `ls | wc -l`  here piping is just like mongodb pipeline here the first output acts like the input for the next command here the ls will tell you all the files and directories and wc -l gonna count all of them 
            1. `ls | grep host` count all ls all the files and directories and show me all the files that starts with the name host 
15. # users and groups
  - users and groups are used to control access to files and resources 
  - users login to the system by supplying their username and pasword
  - every user of teh system is assigned a unique user ID number (the UID)
  - Users name and UID are stored in etc/passwd
  `uid=1000(vagrant) gid=1000(vagrant) groups=1000(vagrant)`
  - uid is the user Id gid is the group id 
  - so vagrant user belongs to the group called vagrant and a group called wheel
  - `useraadd {name}` this command is used to create an user 
  - `tail -4 /etc/passwd` gives us the information about the users
   - `tail -4 /etc/group` gives you the groups that are cerated 
   - `groupadd {group name}` its a way by which you can create a group
16. # File permissions
   -  Viewing permissions from the command line
   - File permissions may be viewed using ls -l
   - Four symbols are used when displaying permissions:
     - `r` : permission to read a file or list a directory contents
     - `w` : permission to write to a file or create and remove files from a directory
     - `x` : permissionto execute a program or change into a directory
     - `- ` : no permission 
     - `ls -l` its gonna give you 
     -rw-------. 1 root root 2027 Mar  5 15:56 anaconda-ks.cfg
     -rw-------. 1 root root 1388 Mar  5 15:56 original-ks.cfg
     now here for the anaconda-ks.cfg it owned by the rooot use and the group is root 
     - => filetype
     rw- => User(permissions)
     --- =>group(for group there is no permissions)
     --- => others(for others there is no permissions)
17. # Sudo
    - sudo gives power to a normal user to execute commands which is owned by root user
    - `sudo yum install git -y` here the normal user is getting the root user powers and therefore if you remove the sudo word this is what you will see `Error: This command has to be run with superuser privileges (under the root user on most systems).`
    - `sudo useradd test` its gonna create a test user if you dont use sudo `useradd: Permission denied. useradd: cannot lock /etc/passwd; try again later.` this is what you will see
    - `useradd test` its gonna create an user now you set pasword for the user using `passwd test` now switch to that user using `su test` 
18. # Software management
    - `tree /var/log` from root user it will show you the tree structure of the directory
    - `curl url -o {file name}` curl is useed to download something say for example curl https://sadas -o rpmfinder
    - `rpm -ivh rpmfinder` this one is for installing where i stands for install , v stands for verbose (for printing) , h is for human readable
    - `yum install httpd` here the thing is most of teh times the packages have interanal dependencies so its better to use yum as its gonna install teh target package as well as its dependencies
    - `yum remove httpd` if you want to remove the package simply use httpd
    - 