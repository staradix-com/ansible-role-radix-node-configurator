Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder ".", "/vagrant/roles/radix-node-configurator"
  
    config.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus = 4
      v.name = "radix-node-configurator"
    end

    config.vm.disk :disk, name: "/opt/radixdlt", size: "100GB"

    $docker_install_script = <<-SCRIPT
      curl -fsSL https://get.docker.com -o get-docker.sh
      sudo sh get-docker.sh
      curl -s -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose && ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
      usermod -aG docker vagrant && usermod -aG docker vagrant && \
      systemctl enable docker --now
    SCRIPT

    $script = <<-SCRIPT
      sudo apt-get update
      sudo apt-get install -y software-properties-common
      sudo apt-add-repository ppa:ansible/ansible -y
      sudo apt-get install -y ansible python3-pip ca-certificates curl gnupg lsb-release

      cd /vagrant/roles/radix-node-configurator && pip3 install -r requirements.txt
      sudo cp /vagrant/roles/radix-node-configurator/tests/*  /vagrant

      sudo reboot now
    SCRIPT

    config.vm.provision "shell", inline: $docker_install_script, privileged: true
    config.vm.provision "shell", inline: $script, privileged: false

  end
