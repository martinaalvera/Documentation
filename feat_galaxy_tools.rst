Galaxy ShedTools
================

Each Galaxy instance is customizable, through the web front-end, with different sets of pre installed tools (e.g. SAMtools, BamTools, Bowtie, MACS, RSEM, etc...), exploiting CONDA as default dependency resolver.

New Tools automatically installed using the official GalaxyProject python library `Ephemeris <https://ephemeris.readthedocs.io/en/latest/index.html>`_.

Current possible pre-sets:

#. galaxy-NGS_: Galaxy ready for NGS analysis.
#. galaxy-RNAseq_: Galaxy ready for RNA Sequencing analysis (original galaxy flavor `here <https://github.com/bgruening/galaxy-rna-seq/blob/master/rna_seq_tools.yml>`_).
#. galaxy-TESTING_: Galaxy test recipe.
#. galaxy-REVIEW_: Galaxy for INDIGO Review.

.. _galaxy-NGS: https://github.com/indigo-dc/Galaxy-flavors-recipes/blob/master/galaxy-flavors/galaxy-NGS-tool-list.yml)
.. _galaxy-RNAseq: https://github.com/indigo-dc/Galaxy-flavors-recipes/blob/master/galaxy-flavors/galaxy-RNAseq-tool-list.yml
.. _galaxy-TESTING: https://github.com/indigo-dc/Galaxy-flavors-recipes/blob/master/galaxy-flavors/galaxy-TESTING-tool-list.yml
.. _galaxy-REVIEW: https://github.com/indigo-dc/Galaxy-flavors-recipes/blob/master/galaxy-flavors/galaxy-REVIEW-tool-list.yml

The corresponding recipe on github is downloaded and processed. It is possible to easily add new flavors, just adding new recipes on github.

Create and test Galaxy flavors
------------------------------
For each tool you want to install, you must provide tool ``name`` and ``owner`` and one between ``tool_panel_section_id`` and ``tool_panel_section_label``.

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

For instance, this is the galaxy TESTING recipe:

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

Conda support
-------------




References
----------

Galaxy flavors


Ephemeris: https://ephemeris.readthedocs.io/en/latest/
Ephemeris documentation: https://github.com/galaxyproject/ephemeris
Conda for Galaxy tools dependencies: https://docs.galaxyproject.org/en/master/admin/conda_faq.html
