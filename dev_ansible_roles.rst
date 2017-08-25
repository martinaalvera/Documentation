Galaxycloud Ansible Roles
=========================
Ansible automates Galaxy (postgresql, NGINX, uWSGI, proftpd) installation and configuration using YAML syntax.

These roles make extensive use of Ansible Modules, which are the ones that do the actual work in ansible, they are what gets executed in each playbook task.
Furthermore, a python scripts collection for galaxy advanced configuration is used (run by ansible).

Ansible roles documentation
---------------------------

.. toctree::
   :maxdepth: 2

   ansible_galaxycloud
   ansible_galaxycloud-os
   ansible_galaxycloud-refdata
   ansible_galaxy-tools
   ansible_cvmfs_server
   ansible_cvmfs_client
