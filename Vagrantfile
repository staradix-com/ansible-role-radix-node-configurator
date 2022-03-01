Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder ".", "/vagrant/roles/radix-node-configurator"
  
    config.vm.provider "virtualbox" do |v|
      v.memory = 8192
      v.cpus = 4
      v.name = "radix-node-configurator"
    end

    config.vm.disk :disk, name: "/opt/radixdlt", size: "100GB"

    $script = <<-SCRIPT
      sudo apt-get update
      sudo apt-get install -y software-properties-common
      sudo apt-add-repository ppa:ansible/ansible -y
      sudo apt-get install -y ansible python3-pip ca-certificates curl gnupg lsb-release

      ansible-galaxy install geerlingguy.docker
      ansible localhost -m include_role -a name=geerlingguy.docker
      
      sudo cp /vagrant/roles/radix-node-configurator/tests/*  /vagrant
      cd /vagrant && ansible-playbook test.yml -i inventory.yml
    SCRIPT

    config.vm.provision "shell", inline: $script, privileged: false

  end
