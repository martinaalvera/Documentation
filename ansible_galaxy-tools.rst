Galaxy-tools
============
This ansible role has been cloned from the official `galaxyproject.galaxy-tools <https://github.com/galaxyproject/ansible-galaxy-tools>`_, with small changes.

This Ansible role is for automated installation of tools from a Tool Shed into Galaxy.

When run, this role will create an execution environment, install ephemeris and invoke the shed-install command to install desired tools into Galaxy. The list of tools to install is provided in files/tool_list.yaml file.

Example Playbook
----------------

To use the role, you need to create a playbook and include the role in it. 

::

  - hosts: localhost
    gather_facts: False
    connection: local
    vars:
        galaxy_tools_tool_list_files: [ "files/sample_tool_list.yaml" ]
        galaxy_tools_galaxy_instance_url: http://127.0.0.1:8080/
        # galaxy_tools_api_key: <API key for Galaxy admin user>
    roles:
      - indigo-dc.galaxy-tools


Example Tool list
-----------------
For each tool you want to install, you must provide tool ``name`` and ``owner`` and one between ``tool_panel_section_id`` and ``tool_panel_section_label`` in the yaml tool list.

::

  ---
  api_key: <Admin user API key from galaxy_instance>
  galaxy_instance: <Galaxy instance IP>

  tools:
  - name: fastqc
    owner: devteam
    tool_panel_section_label: 'Tools'
    install_resolver_dependencies: True
    install_tool_dependencies: False

  - name: 'bowtie_wrappers'
    owner: 'devteam'
    tool_panel_section_label: 'Tools'
    install_resolver_dependencies: True
    install_tool_dependencies: False


Variables
---------

Required variables
******************
Only one of the two variables is requried (if both are set, the API key takes precedence and a bootstrap user is not created):

``galaxy_tools_api_key``: the Galaxy API key for an admin user on the target Galaxy instance (not required if the bootstrap user is being created)

``galaxy_tools_admin_user_password``: a password for the Galaxy bootstrap user (required only if galaxy_install_bootstrap_user variable is set)

Optional variables
******************
See defaults/main.yml for the available variables and their defaults.

Control flow variables
**********************
The following variables can be set to either yes or no to indicate if the given part of the role should be executed:

``galaxy_tools_install_tools``: (default: yes) whether or not to run the tools installation script

``galaxy_tools_create_bootstrap_user``: (default: no) whether or not to create a bootstrap Galaxy admin user

``galaxy_tools_delete_bootstrap_user``: (default: no) whether or not to delete a bootstrap Galaxy admin user

References
----------

galaxyproject.galaxy-tools: https://github.com/galaxyproject/ansible-galaxy-tools

Ephemeris: https://github.com/galaxyproject/ephemeris

galaxy-tools-playbook: https://github.com/afgane/galaxy-tools-playbook

