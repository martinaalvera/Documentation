GalaxyCloud Documentation
=========================

.. _fig_updateprocess:

.. figure:: _static/elixir_italy_logo.png
   :scale: 10 %
   :align: center
   :alt: elixir-italy logo

Galaxy as a Cloud Service (conversely GalaxyCloud) provides the possibility to automate the creation of Galaxy-based virtualized environments through an easy setup procedure, providing an on-demand workspace ready to be used by life scientists and bioinformaticians.

Galaxy is a workflow manager adopted in many life science research environments in order to facilitate the interaction with bioinformatics tools and the handling of large quantities of biological data.

Once deployed each Galaxy instance will be fully customizable with tools and reference data and running in an insulated environment, thus providing a suitable platform for research, training and even clinical scenarios involving sensible data. Sensitive data requires the development and adoption of technologies and policies for data access, including e.g. a robust user authentication platform.

For more information on the Galaxy Project, please visit the https://galaxyproject.org

GalaxyCloud has been developed by ELIXIR-IIB, the italian node of ELIXIR, within the INDIGO-DataCloud project (H2020-EINFRA-2014-2) which aims to develop PaaS based cloud solutions for e-science.

.. Note::

  GalaxyCloud is in fast development. For this reason the code and the documentation may not always be in sync. We try to make our best to have good documentatation. Sorry for that. 

.. toctree::
   :maxdepth: 2
   :caption: Introduction

   intro_overview
   intro_architecture
   intro_elixir-it
   intro_indigo


.. toctree::
   :maxdepth: 2
   :caption: Quickstarts

   qs_galaxy
   qs_galaxy_express
   qs_isolate_your_galaxy
   qs_galaxy_cluster
   qs_galaxy_onedata
   qs_virtual_hdw_presets

.. toctree::
   :maxdepth: 2
   :caption: Features

   feat_galaxy_custom
   feat_galaxy_prod_env
   feat_instance_isolation
   feat_galaxy_tools
   feat_reference_data
   feat_cluster_support
   feat_authentication
   feat_validation

.. toctree::
   :maxdepth: 2
   :caption: Galaxy admin

   script_galaxyctl_libs
   script_galaxyctl
   script_luksctl
   script_onedatactl

.. toctree::
   :maxdepth: 2
   :caption: Development

   dev_ansible_roles
   dev_tosca_templates
   dev_build_cvmfs_server


.. toctree::
   :maxdepth: 2
   :caption: Included INDIGO components

   indigo_orchestrator
   indigo_im
   indigo_fgw
   indigo_onedata
   indigo_clues

Tutorials
---------

Galaxy For Developers: https://crs4.github.io/Galaxy4Developers/

Support
-------
Github issues: https://github.com/mtangaro/GalaxyCloud/issues

Articles
--------


Cite
----


Indices and tables
------------------

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
