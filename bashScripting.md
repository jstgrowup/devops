# Bash Scripting

- Bash script will tell what commands to execute
- `vagrant ssh scriptbox` to login to scriptbox vm
- `vi /etc/hostname`

# First script

- `mkdir /opt/scripts` create a folder named as scripts
- `vim firstscript.sh` to create a shell script file

## Format

- #!/bin/bash => this tells that go to this location and read the commands #! (shabang) so open this file and execute the interpretor
- `echo` its for printing
- `echo "welcome to bash script"
echo "the uptime of the system is:"
uptime
echo "memory utilization"
free -m
echo "Disk utilization"
df -h` this is the first script
- `chmod +x firstscript.sh` to add the executable permissions to the file so that i can execute it
-
