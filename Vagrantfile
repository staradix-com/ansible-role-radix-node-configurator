Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder ".", "/vagrant/roles/radix-node-configurator"
  
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.name = "radix-node-configurator"
    end

    config.vm.disk :disk, name: "/opt/radixdlt", size: "100GB"

    $script = <<-SCRIPT
    # Install Ansible and it's dependencies
    sudo apt-get update
    sudo apt-get install -y software-properties-common
    sudo apt-add-repository ppa:ansible/ansible -y
    sudo apt-get install -y ansible python3-pip ca-certificates curl gnupg lsb-release

    # Download and install Docker
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update && sudo apt-get install -y docker-ce docker-ce-cli containerd.io
    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose && sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

    # Install role dependencies and copy Ansible files
    cd /vagrant/roles/radix-node-configurator && pip3 install -r requirements.txt
    sudo cp /vagrant/roles/radix-node-configurator/tests/*  /vagrant

    # Add user to Docker group, make sure Docker is started
    sudo usermod -aG docker vagrant && exec sudo su -l $USER
    sudo systemctl enable docker --now && \

    # Run the playbook
    cd /vagrant && ansible-playbook test.yml -i inventory.yml
    SCRIPT

    config.vm.provision "shell", inline: $script, privileged: false

  end
