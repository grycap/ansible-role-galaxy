[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)  
[![Build Status](https://travis-ci.org/grycap/ansible-role-galaxy.svg?branch=master)](https://travis-ci.org/grycap/ansible-role-galaxy)

Galaxy Portal Role
==================

Install [Galaxy Portal](https://galaxyproject.org/).

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

	# Galaxy node type: portal or wn
	galaxy_node_type: portal
	# Path to install the Galaxy software
	galaxy_install_path: /opt/galaxy
	# Galaxy version to install
	GALAXY_VERSION: 16.01
	# Type of LRMS to use (Currently only supported local , slurm or torque)
	galaxy_lrms: local
	# E-mail of the admin user
	galaxy_admin: admin@admin.com
	# API key for admin user
	galaxy_admin_api_key: not_very_secret_api_key
	# User to launch the Galaxy portal
	galaxy_user: galaxy
	# User ID to assing to the galaxy user
	GALAXY_USER_ID: 4001
	# Password to assing to the user (galaxy+00)
	# See http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module for more info
	GALAXY_USER_PASSWORD: $6$d6becl8ohu0F4$Pzf2NIrfhGVvoGzaqf6aPEDhYi5ZTbmujF0oGv7qGNxXwHOKqfehm197YzEGZqJ4lwxDL5jWU6goqeaMHic3s0
	# Specify if at the end of the installation the Galaxy portal is launched as daemon
	GALAXY_LAUNCH_DAEMON: true

---
	# Galaxy node type: portal or wn
	galaxy_node_type: portal
	# Type of LRMS to use (Currently only supported local, slurm or torque)
	galaxy_lrms: local
	# E-mail of the admin user
	galaxy_admin: admin@admin.com
	# Password of the admin user
	galaxy_admin_password: adminpass
	# API key for admin user
	galaxy_admin_api_key: not_very_secret_api_key
	# User to launch the Galaxy portal
	galaxy_user: galaxy
	# User ID to assing to the galaxy user
	GALAXY_USER_ID: 1450
	# Password to assing to the user (galaxy+00)
	# See http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module for more info
	GALAXY_USER_PASSWORD: $6$d6becl8ohu0F4$Pzf2NIrfhGVvoGzaqf6aPEDhYi5ZTbmujF0oGv7qGNxXwHOKqfehm197YzEGZqJ4lwxDL5jWU6goqeaMHic3s0
	# Password used to derive a munge key for authentication between the server and the workers.
	galaxy_munge_key_password: ''
	# Slurm server name
	galaxy_slurm_server_name: slurmserver
	# Galaxy export dir
	galaxy_export_dir: /mnt/export
	# ENV variables for the Docker Galaxy
	galaxy_docker_env_vars:
	   NONUSE: reports
	   GALAXY_LOGGING: full
	   DOCKER_PARENT: True
	   GALAXY_CONFIG_HOST: 0.0.0.0
	   GALAXY_DEFAULT_ADMIN_USER: "{{galaxy_admin}}"
	   GALAXY_DEFAULT_ADMIN_PASSWORD: "{{galaxy_admin_password}}"
	   GALAXY_DEFAULT_ADMIN_KEY: "{{galaxy_admin_password}}"
	   GALAXY_CONFIG_ADMIN_USERS: "{{galaxy_admin}}"
	   GALAXY_CONFIG_MASTER_API_KEY: "{{galaxy_admin_api_key}}"

	# ENV variables for the Docker Galaxy in case of using slurm
	slurm_galaxy_docker_env_vars:
	   NONUSE: slurmctld,reports
	   GALAXY_CONFIG_JOB_CONFIG_FILE: "/export/slurm_job_conf.xml"

	galaxy_docker_volumes:
	  - "/var/run/docker.sock:/var/run/docker.sock"
	  - "{{galaxy_export_dir}}:/export/"
	  - "/etc/nginx/nginx.conf:/etc/nginx/nginx.conf"
	  - "/etc/nginx/uwsgi.conf:/etc/nginx/conf.d/uwsgi.conf"

	slurm_galaxy_docker_volumes:
	  - "{{galaxy_export_dir}}/slurm.conf:/etc/slurm-llnl/slurm.conf"


Example Playbook
----------------

This an example of how to install the Galaxy portal version 16.01 in the path /opt/galaxy:

    - hosts: servers
      roles:
         - { role: grycap.galaxy, GALAXY_VERSION: 16.01,  galaxy_install_path: /opt/galaxy}
