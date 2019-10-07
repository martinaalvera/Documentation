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

   introduction/laniakea
   introduction/architecture
   introduction/elixir_it
   introduction/indigo

.. toctree::
   :maxdepth: 2
   :caption: user documentation

   user_documentation/galaxy/galaxy
   user_documentation/encryption/manage_encrypted_instance
   qs_galaxy_cluster
   user_documentation/ssh_keys/ssh_keys.rst
   user_documentation/galaxy/virtual_hdw_presets
   user_documentation/galaxy_production_environment/galaxy_production_environment
   feat_galaxy_tools
   feat_reference_data
   feat_cluster_support
   user_documentation/authentication/authentication
   user_documentation/faq/faq

.. toctree::
   :maxdepth: 2
   :caption: admin documentation

   admin_documentation/encryption/encryption
   script_galaxyctl_libs
   script_galaxyctl
   script_luksctl
   dev_ansible_roles
   admin_documentation/tosca_templates/tosca_templates
   admin_documentation/cvmfs/build_cvmfs_server
   admin_documentation/vault/vault_config
   admin_documentation/dashboard/dashboard_config
   admin_documentation/indigo_paas_deploy/introduction

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
