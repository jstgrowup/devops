1. # vagrant IP, RAM & CPU
   - when you go inside the vagrant there will be be a vagrant file
   - so all the configuration will be written there 
 - config.vm.provider "virtualbox" do |vb|
     Display the VirtualBox GUI when booting the machine
    vb.gui = true

    Customize the amount of memory on the VM:
     vb.memory = "1600"
  end
  - her in vb.memory you can edit it and  increase the memory but you need to reload the VM again after the configuratiuon changes , this is also known as subblock
  - `config.vm.network "private_network", ip: "192.168.33.10"` to assign a static IP to the VM
2. # Vgrant sync directories
  - so if i create anything or any files in my VM the files will apear in the host machine
3. # provisioning
  - its the process of executing commands when the VMs comesup