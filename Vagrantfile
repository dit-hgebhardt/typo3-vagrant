# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off off
  config.vm.box = "ipf-precise"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "2048"]
    v.vm.box_url = "http://files.vagrantup.com/precise32.box"
  end

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  # config.vm.network :hostonly, "192.168.33.10"

  # Assign this VM to a bridged network, allowing you to connect directly to a
  # network using the host's network device. This makes the VM appear as another
  # physical device on your network.
  # config.vm.network :bridged

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  #config.vm.forward_port 80, 8333
  config.vm.network "forwarded_port", guest: 80, host: 8333

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  # config.vm.share_folder "v-data", "/vagrant_data", "../data"


  config.vm.provider "vmware_fusion" do |v,override|
  	override.vm.box = "ipf-precise-vmware"
    v.vmx["memsize"] = "2048"
    v.vmx["numvcpus"] = "2"
    override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
  end

  config.vm.provider "vmware_workstation" do |v,override|
  	override.vm.box = "ipf-precise-vmware"
    v.vmx["memsize"] = "2048"
    v.vmx["numvcpus"] = "2"
    override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
  end

   config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "./cookbooks"
    #chef.log_level = :debug
    chef.json = {
      "mysql" => {
        "server_root_password" => "typo3",
		"server_debian_password" => "typo3",
		"server_repl_password" => "typo3"
      }
    }
    chef.add_recipe("typo3")
    chef.add_recipe("mysql::server")
   end

end
