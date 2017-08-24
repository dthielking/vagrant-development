# -*- mode: ruby -*-
# vi: set ft=ruby :

suffix="dev01"
fqdn="local"
source_git_repository="C:/Users/Thielking/Documents/git"
username="ubuntu"

# Provisioning Variables
playbook="provisoning/playbook.yaml"
galaxy_role_file="provisoning/requirements.yaml"

Vagrant.configure("2") do |config|

  # User debian/contrig-jessie64 Template
  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  if !(source_git_repository == "")
    config.vm.synced_folder "#{source_git_repository}", "/home/#{username}/git", type: "virtualbox"
  end

  config.vm.define "gui" do |gui|
    config.vm.provider "virtualbox" do |v|
      # Set hostname for vm
      config.vm.hostname = "#{suffix}.#{fqdn}"
      # Set VM name
      v.name = "#{suffix}.#{fqdn}"
      # Display the VirtualBox GUI when booting the machine
      v.gui = true
      # Customize the amount of memory on the VM:
      v.memory = "2048"
      # Enable 3D Acceleration
      v.customize ["modifyvm", :id, "--accelerate3d",  "on"]
      # Set Video Memory to 128MB
      v.customize ["modifyvm", :id, "--vram", "128"]
      # Enable shared Clipboard between Host and VM 
      v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    end
    # Provision of Linux Gui with ansible
    config.vm.provision "ansible_local" do |ansible|
      ansible.install_mode = "pip"
      ansible.playbook = "#{playbook}"
#      ansible.verbose = "-v"
      ansible.galaxy_role_file = "#{galaxy_role_file}"
    end
  end
end
