# -*- mode: ruby -*-
# vi: set ft=ruby :

require "fileutils"

Vagrant.configure(2) do |config|
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end
  config.vm.box_check_update = true
  config.vm.guest = :windows
  config.windows.set_work_network = true
  config.vm.define "vip-win2k12-01" do |d| 
    d.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
    d.vm.hostname =  "vip-win2k12-01"
    d.vm.network "public_network", bridge: "eno4", ip: "192.168.57.77", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    d.vm.provider "virtualbox" do |vb|
      # Don't boot with headless mode
      vb.gui = false
      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus",   "2"]
    end
   end
   if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end
  
