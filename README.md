Radix Node Configurator
=========
Configures a Radix node.  
This is a work in progress. NOT READY FOR PRODUCTION USE.

Requirements
------------
* `ubuntu 20.04`
  
You can try different versions but this is not recommended.  
Radix itself only supports Ubuntu 20.04.  
This repo will not work on other distros.  

Role Variables
--------------
The docker_install boolean (true/false) controls whether the docker install method will be used, or not.
`docker_install: <bool>`

The systemd_install boolean (true/false) controls whether the systemd install method will be used, or not.
`systemd_install: <bool>`

Dependencies
------------
You can find all dependencies in the requirements.txt file.  
Install them with: `pip3 install -r requirements.txt`

Example Playbook
----------------
You can find an example playbook the `tests` directory.  


Local role testing
-------
You can test the role with Vagrant and VirtualBox. Both need to be installed.  
The command is: `VAGRANT_EXPERIMENTAL="cloud_init,disks" vagrant up`  
You need at least: 150GB Disk space, 16GB of RAM free and 4vCPUs.
The docker-compose command will succeed but the core container will keep restarting.

License
-------
* GPLv2

Author Information
------------------

* [info@staradix.com](mailto://info@staradix.com)
* https://staradix.com