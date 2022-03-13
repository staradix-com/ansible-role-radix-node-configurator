Radix Node Configurator
=========
Configures a Radix node.  

Releases explained
------------

There are three levels of releases:
* alpha     - Implemented but not tested.
* beta      - Implemented and tested. Only implemented for platforms that are defined in `meta/main.yml`
* stable    - Implemented, tested, and verified idempotent.

Current releases:
------------

Current release: V.1.2
* docker support: beta
* systemd support: alpha

Requirements
------------
* `ubuntu 20.04`
  
You can try different versions but this is not recommended.  
Radix itself only supports Ubuntu 20.04.  
This roll will not work on other distros for now.  

Installing the role
------------

* `ansible-galaxy install stefanfluit.ansible_role_radix_node_configurator`

Role Variables
------------

Good to know: A boolean means that valid values are `true` or `false`.

The docker_install boolean (true/false) controls whether the docker install method will be used, or not.
* `docker_install: <bool>`

The systemd_install boolean (true/false) controls whether the systemd install method will be used, or not.
* `systemd_install: <bool>`

Set this to true if you want to ensure you have the latest version of Radix dependencies.
* `update_radix: <bool>`

Set this to true if you want to ensure you have the latest packages on the host OS.
* `update_ubuntu: <bool>`

Set this to true if you want to see output of the docker commands.
* `debug_output: <bool>`

Enter a valid Radix directory path. Make sure there is 100Gb free space.
For reference, I use `/opt/radix`
* `data_dir: <string>`

Enter a valid Radix username. This is the username that will be used to run Radix commands.
You're best off using `radixdlt`.
* `radix_user: <string>`

Set this to true if u use UFW as a firewall, false if you use iptables.
* `ufw_firewall: <bool>`

Set this to true if you use iptables as a firewall, false if you use UFW.
* `iptables_firewall: <bool>`

Set your region. This determines what node will be used to sync. 
* Valid regions are: eu-west, asia-south, asia-south-east, eu-west, or us-east.
* `radix_node_region: <string>`

Set the radix network ID. 
* Valid values are: `m` or `s`.
* `radix_network_id: <string>`

Set the node type. Setting both to true will cause the playbook to fail.
* `fullnode: <bool>`
* `archive: <bool>`

Make sure to set this to "yes" on first run, and "no" on subsequent runs.
* `new_node: yes/no`

Must be set if new_node is set to "no":
* `keystore_password: <string>`

Dependencies
------------

* You can find all dependencies in the requirements.txt file.  
* Install them with: `pip3 install -r requirements.txt`

Example Playbook
----------------

* You can find an example playbook the `tests` directory.
* `tests/ansible-playbook.yml`


Local role testing
-------
* You can test the role with Vagrant and VirtualBox. Both need to be installed.  
* The command is: `VAGRANT_EXPERIMENTAL="cloud_init,disks" vagrant up`  
* You need at least: 200GB Disk space, 16GB of RAM free and 4vCPUs.
* Note; I use the Vagrant box only to run the playbooks on, usually, a VPS at Hetzner or AWS.

License
-------

* GPLv2

Author Information
------------------

* [info@staradix.com](mailto://info@staradix.com)
* https://staradix.com