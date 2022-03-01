Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder ".", "/vagrant/roles/radix-node-configurator"
  
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.name = "radix-node-configurator"
    end

    config.vm.disk :disk, name: "/opt/radixdlt", size: "100GB"

    $docker_install_script = <<-docker_install_script
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update && sudo apt-get install -y docker-ce docker-ce-cli containerd.io
      curl -s -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose && ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
      usermod -aG docker vagrant
    docker_install_script

    $script = <<-SCRIPT
      sudo apt-get update
      sudo apt-get install -y software-properties-common
      sudo apt-add-repository ppa:ansible/ansible -y
      sudo apt-get install -y ansible python3-pip ca-certificates curl gnupg lsb-release

      cd /vagrant/roles/radix-node-configurator && pip3 install -r requirements.txt
      sudo cp /vagrant/roles/radix-node-configurator/tests/*  /vagrant

      sudo systemctl enable docker --now && \
      cd /vagrant && ansible-playbook test.yml -i inventory.yml
    SCRIPT

    config.vm.provision "shell", inline: $docker_install_script, privileged: true
    config.vm.provision "shell", inline: $script, privileged: false

  end
