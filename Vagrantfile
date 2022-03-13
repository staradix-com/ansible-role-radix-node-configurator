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
      echo "export PATH=\"$HOME/.local/bin:$PATH\"" >> ~/.bashrc
      pip3 install --upgrade pip && pip3 install docker-compose

      ansible-galaxy install geerlingguy.docker || true
      
      sudo cp /vagrant/roles/radix-node-configurator/tests/*  /vagrant
      sudo chown -R vagrant:vagrant /vagrant
      cp /vagrant/key /home/vagrant/.ssh/id_ed25519 && chown vagrant:vagrant /home/vagrant/.ssh/id_ed25519 && chmod 600 /home/vagrant/.ssh/id_ed25519
      eval `ssh-agent -s` && ssh-add /home/vagrant/.ssh/id_ed25519

      wget https://raw.githubusercontent.com/docker/docker-py/master/docker/errors.py -O /tmp/errors.py
      sudo cp /tmp/errors.py /usr/local/lib/python3.8/dist-packages/docker/errors.py
    SCRIPT

    config.vm.provision "shell", inline: $script, privileged: false

  end
