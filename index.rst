|project_name| Documentation
============================

.. _fig_updateprocess:

.. figure:: _static/elixir_italy_logo.png
   :scale: 10 %
   :align: center
   :alt: elixir-italy logo

|project_name| provides the possibility to automate the creation of Galaxy-based virtualized environments through an easy setup procedure, providing an on-demand workspace ready to be used by life scientists and bioinformaticians.

Galaxy is a workflow manager adopted in many life science research environments in order to facilitate the interaction with bioinformatics tools and the handling of large quantities of biological data.

Once deployed each Galaxy instance will be fully customizable with tools and reference data and running in an insulated environment, thus providing a suitable platform for research, training and even clinical scenarios involving sensible data. Sensitive data requires the development and adoption of technologies and policies for data access, including e.g. a robust user authentication platform.

For more information on the Galaxy Project, please visit the https://galaxyproject.org

|project_name| has been developed by ELIXIR-IIB, the italian node of ELIXIR, within the INDIGO-DataCloud project (H2020-EINFRA-2014-2) which aims to develop PaaS based cloud solutions for e-science.

.. Note::

   |project_name| is in fast development. For this reason the code and the documentation may not always be in sync. We try to make our best to have good documentatation 

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

   qs_galaxy_vm
   qs_galaxy
   qs_encryption
   qs_galaxy_cluster
   qs_key_pair
   qs_virtual_hdw_presets

.. toctree::
   :maxdepth: 2
   :caption: Features

   feat_options
   feat_galaxy_prod_env
   feat_instance_isolation
   feat_galaxy_tools
   feat_reference_data
   feat_cluster_support
   feat_auth
   feat_validation

.. toctree::
   :maxdepth: 2
   :caption: Galaxy admin

   script_galaxyctl_libs
   script_galaxyctl
   script_luksctl
   script_onedatactl
   faq

.. toctree::
   :maxdepth: 2
   :caption: Development

   dev_ansible_roles
   dev_tosca_templates
   dev_build_cvmfs_server
   vault/vault_config

.. toctree::
   :maxdepth: 2
   :caption: Laniakea Installation

   indigo_paas_deploy/introduction
   indigo_paas_deploy/prerequisites
   indigo_paas_deploy/iam
   indigo_paas_deploy/proxy
   indigo_paas_deploy/im
   indigo_paas_deploy/cmdb
   indigo_paas_deploy/slam
   indigo_paas_deploy/orchestrator
   indigo_paas_deploy/vault
   indigo_paas_deploy/dashboard

.. toctree::
   :maxdepth: 2
   :caption: FAQ INDIGO components

   indigo_paas_deploy/orchestrator_faq
   indigo_paas_deploy/im_faq
   indigo_paas_deploy/clues_faq

GitHub repository
-----------------
https://github.com/Laniakea-elixir-it

DockerHub repository
--------------------
https://hub.docker.com/r/laniakeacloud

Support
-------

If you need support please contact us to: ``laniakea.helpdesk@gmail.com``

Software glitches and bugs can occasionally be encoutered. The best way to report a bug is to open an issue on our GitHub `repository <https://github.com/Laniakea-elixir-it/elixir-italy-science-gateway/issues>`_.

Cite
----

Licence
-------
GNU General Public License v3.0+ (https://www.gnu.org/licenses/gpl-3.0.txt)

Galaxy tutorials
----------------
Galaxy training network: https://galaxyproject.org/teach/gtn/

Galaxy For Developers: https://crs4.github.io/Galaxy4Developers/

Indices and tables
------------------
* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
