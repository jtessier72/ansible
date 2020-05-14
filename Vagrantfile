# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
   config.vm.box = "ubuntu/bionic64"
   #config.vm.box = "debian/jessie64"
  
   config.vm.provider :virtualbox do |v|
     v.name = "epsilon.dev"
     v.memory = 2048
     v.cpus = 2

     Drives = [2,3,4,5]
     Drives.each do |hd|

       path_to_disk = "/tmp/disk#{hd}.vdi"
       unless File.exist?(path_to_disk)
         v.customize ['createhd', '--filename', path_to_disk,'--variant', 'Fixed', '--size', 5 * 1024]
         v.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', hd, '--device', 0, '--type', 'hdd', '--medium', path_to_disk]
       end
     end

     #Drives = [2,3,4,5]
     #Drives.each do |hd|
     #  puts "harddrive #{hd}"
     #  v.customize ['createhd', '--filename', "tmp/disk#{hd}.vdi",'--variant', 'Fixed', '--size', 5 * 1024]
     #  v.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', hd, '--device', 0, '--type', 'hdd', '--medium', "tmp/disk#{hd}.vdi"]  
     #end
   end
  
   config.vm.provision :ansible do |ansible|
     ansible.verbose = "vvv"
#     ansible.extra_vars = { "ansible_python_interpreter" => "/usr/bin/python2" }
     ansible.extra_vars = { "ansible_python_interpreter" => "/usr/bin/python3" }
     ansible.playbook = "main.yml"
   end
end
