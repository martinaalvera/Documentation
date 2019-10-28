Laniakea Ansible Roles
======================

Ansible automates Galaxy installation and configuration using Ansible roles. These roles make extensive use of Ansible Modules, which are the ones that do the actual work in ansible, they are what gets executed in each playbook task. Furthermore, a python scripts collection for galaxy advanced configuration is used (run by ansible).

.. note::

   All roles can be easily installed through ``ansible-galaxy``.

-------------------------
``indigo-dc.galaxycloud``
-------------------------

:Description:
	Install Galaxy Production environment, i.e. Galaxy with all needed softaware, PostgreSQL, NGINX, Proftpd and uWSGI. The role also installs `Galaxyctl and its API <https://github.com/Laniakea-elixir-it/galaxyctl>`_ for Galaxy management.

:Installation:
	::

	  # ansible-galaxy install indigo-dc.galaxycloud 

:Github:
	https://github.com/indigo-dc/ansible-role-galaxycloud

----------------------------
``indigo-dc.galaxycloud-os``
----------------------------

:Description:
	This role provides storage encryption with aes-xts-plain64 algorithm using LUKS for Galaxy instances. The role installs and run `fast-luks <https://github.com/Laniakea-elixir-it/fast-luks>`_ for storage encryption, and `LUKSctl <https://github.com/Laniakea-elixir-it/luksctl>`_ and `LUKSctl APIs <https://github.com/Laniakea-elixir-it/luksctl_api>`_ for storage management.

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud-os

:Github:
	https://github.com/indigo-dc/ansible-role-galaxycloud-os

-------------------------------
``indigo-dc.galaxycloud-tools``
-------------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud-tools

:Github:

----------------------------------
``indigo-dc.galaxycloud-refdata``
----------------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud-refdata

:Github:


------------------------------------
``indigo-dc.galaxycloud-fastconfig``
------------------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud-fastconfig

:Github:

--------------------------------
``indigo-dc.galaxycloud_docker``
--------------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud_docker

:Github:

--------------------------------
``indigo-dc.galaxycloud_docker``
--------------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.galaxycloud_docker

:Github:


-------------------------
``indigo-dc.cvmfs-client``
-------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.cvmfs-client

:Github:

-------------------------
``indigo-dc.cvmfs-server``
-------------------------

:Description:

:Installation:
        ::

          ansible-galaxy install indigo-dc.cvmfs-server

:Github:
