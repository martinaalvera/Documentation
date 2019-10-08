Create and test Galaxy flavours
===============================

To create a new Galaxy flavour, a tool list file, written in YAML syntax, has to be provided. For example, the following recipe can be used to install fastqc and bowtie:

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

For each tool to install, ``name`` and ``owner`` and one between ``tool_panel_section_id`` and ``tool_panel_section_label`` must be provided.

====================================  =====================================  ====================================  ========================================
Keys                                  Required                               Default value                         Description
====================================  =====================================  ====================================  ========================================
``name``                              yes                             				                   This is is the name of the tool to install
``owner``                             yes                             				                   Owner of the Tool Shed repository from where the tools is being installed
``tool_panel_section_id``             yes, if ``tool_panel_section_label``                                         ID of the tool panel section where you want the
                                      not specified		                                                   tool to be installed. The section ID can be found
			                                                                                           in Galaxy's ``shed_tool_conf.xml`` config file. Note
                                    			                                                           that the specified section must exist in this file.
 					                                                                           Otherwise, the tool will be installed outside any
                                                                                                                   section.
``tool_panel_section_label``          yes, if ``tool_panel_section_id``                                            Display label of a tool panel section where
                                      not specified                                                                you want the tool to be installed. If it does not
                                                                                                                   exist, this section will be created on the target
                                                                                                                   Galaxy instance (note that this is different than
                                                                                                                   when using the ID).
                                                                                                                   Multi-word labels need to be placed in quotes.
                                                                                                                   Each label will have a corresponding ID created;
                                                                                                                   the ID will be an all lowercase version of the
                                                                                                                   label, with multiple words joined with
                                                                                                                   underscores (e.g., 'BED tools' -> 'bed_tools').
``tool_shed_url``                                                            ``https://toolshed.g2.bx.psu.edu)``   The URL of the Tool Shed from where the tool should be
                                                                                                                   installed.
``revisions``                                                                latest                                A list of revisions of the tool, all of which will attempt to
                                                                                                                   be installed.
``install_tool_dependencies``                                                True                                  True or False - whether to install tool
                                                                                                                   dependencies or not.
``install_repository_dependencies``                                          True                                  True or False - whether to install repo
                                                                                                                   dependencies or not, using classic toolshed packages
====================================  =====================================  ====================================  ========================================

Conda support
-------------
Conda is a package manager like apt-get, yum, pip, brew or guix and it is, currently, used as default dependency resolver in Galaxy.

References
----------

`Galaxy flavors <https://github.com/bgruening/docker-galaxy-stable#Extending-the-Docker-Image>`_

`Ephemeris <https://ephemeris.readthedocs.io/en/latest/>`_

`Ephemeris documentation <https://github.com/galaxyproject/ephemeris>`_

`Conda for Galaxy tools dependencies <https://docs.galaxyproject.org/en/master/admin/conda_faq.html>`_
