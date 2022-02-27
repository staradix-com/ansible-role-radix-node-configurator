Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
  
    config.vm.synced_folder ".", "/vagrant/radix-node-configurator"
    config.vm.synced_folder "/home/fluit/ansible-tmp", "/vagrant"
  
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end

    config.vm.disk :disk, name: "/opt/radix", size: "200GB"
    config.vm.network "public_network", bridge: 'enp5s0', ip: '192.168.178.187'

    $script = <<-SCRIPT
    sudo apt-get update
    sudo apt-get install -y software-properties-common
    sudo apt-add-repository ppa:ansible/ansible -y
    sudo apt-get install -y ansible
    SCRIPT

    config.vm.provision "shell", inline: $script, privileged: false

  end
  