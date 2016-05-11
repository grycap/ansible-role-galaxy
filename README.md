Galaxy Portal Role 
==================

Install Galaxy Portal [1]. This role has been specifically developed to be used in the INDIGO project.

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

	# Path to install the Galaxy software
	galaxy_install_path: /opt/galaxy
	# Galaxy version to install
	GALAXY_VERSION: v16.01
	# Type of LRMS to use (Currently only supported local or torque)
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

Example Playbook
----------------

This an example of how to install the Galaxy portal version 16.01 in the path /opt/galaxy:

    - hosts: servers
      roles:
         - { role: indigo-dc.galaxy, GALAXY_VERSION: v16.01,  galaxy_install_path: /opt/galaxy}

License
-------

Apache Licence v2 [2]

[1] https://galaxyproject.org/

[2] http://www.apache.org/licenses/LICENSE-2.0
