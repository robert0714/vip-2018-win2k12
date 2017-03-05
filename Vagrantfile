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
    default_router = "192.168.57.1"
    # change/ensure the default route via the local network's WAN router, useful for public_network/bridged mode
    d.vm.provision :shell, inline: "netsh int ip set address 'Ethernet 2' address=192.168.57.77 mask=255.255.255.0 gateway=192.168.57.1"
    d.vm.provision :shell, inline: "net user jboss  abc!123  /ADD"
    d.vm.provision :shell, inline: "net localgroup administrators jboss /add"
    #netsh int ip set address 'Ethernet 2' address=192.168.57.77 mask=255.255.255.0 gateway=192.168.57.1
    d.vm.provider "virtualbox" do |vb|
      # Don't boot with headless mode
      vb.gui = false
      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus",   "2"]
      vb.memory = 8192
    end
   end
   config.vm.define "vip-win2k12-02" do |d| 
    d.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
    d.vm.hostname =  "vip-win2k12-02"
    d.vm.network "public_network", bridge: "eno4", ip: "192.168.57.78", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    default_router = "192.168.57.1"
    # change/ensure the default route via the local network's WAN router, useful for public_network/bridged mode
    d.vm.provision :shell, inline: "netsh int ip set address 'Ethernet 2' address=192.168.57.78 mask=255.255.255.0 gateway=192.168.57.1"
    d.vm.provision :shell, inline: "net user jboss  abc!123  /ADD"
    d.vm.provision :shell, inline: "net localgroup administrators jboss /add"
    #netsh int ip set address 'Ethernet 2' address=192.168.57.77 mask=255.255.255.0 gateway=192.168.57.1
    d.vm.provider "virtualbox" do |vb|
      # Don't boot with headless mode
      vb.gui = false
      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus",   "2"]
      vb.memory = 8192
    end
   end
   if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end
  
