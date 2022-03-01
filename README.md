Radix Node Configurator
=========

Configures a Radix node.  
This is a work in progress. NOT READY FOR PRODUCTION USE.

Requirements
------------

* Docker API >= 1.20
* Docker SDK for Python >= 1.8.0
* PyYAML >= 3.11
* docker-compose >= 1.7.0, < 2.0.0
* Ansible >= 2.9

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

License
-------

* GPLv2

Author Information
------------------

* info@staradix.com
* http://staradix.com
