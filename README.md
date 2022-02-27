Radix Node Configurator
=========

Configures a Radix node

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

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
