Get |galaxy_latest| 
===================

The Galaxy section allows user to deploy a full `Galaxy production environment <https://galaxyproject.org/admin/config/performance/production-server/>`_.

The service allows to setup and launch a virtual machine configured with the Operative System CentOS 7 and the auxiliary applications needed to support a Galaxy production environment such as PostgreSQL, Nginx, uWSGI and Proftpd and to deploy the Galaxy platform itself and the selected Galaxt tools.

.. Warning::

   Everything is configured on the fly and, depending on the number of the tools to be installed may take time.

.. seealso::

   For a detailed descreption of all Web UI options see section: :doc:`feat_options`.

.. seealso::

   To login into the portal see section: :doc:`feat_auth`.

Instantiate |galaxy_latest|
---------------------------

#. Enter the |galaxy_latest| section:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_FGW.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express main window

#. Set your ``job identifier`` as you prefer, which will identfy your Galaxy in the job list, once your request is submitted:

   .. Note::

      Please be descriptive in the ``job Identifier`` section, storing the Galaxy VM features, like user, VCPUs and Memory, tools presets and storage.

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_JobID.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Select your instance flavour (virtual CPUs and the memory size):

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_VirtualHardware.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

   Currently, the following pre-sets are available:

   =========  =======  =======  =============  =============
   Name       VCPUs    RAM      Total Disk     Root Disk
   =========  =======  =======  =============  =============
   small      1        2 GB     20 GB          20 GB
   medium     2        4 GB     20 GB          20 GB
   large      4        8 GB     20 GB          20 GB
   xlarge     8        16 GB    20 GB          20 GB
   xxlarge    16       32 GB    20 GB          20 GB
   =========  =======  =======  =============  =============

#. Copy & Past your SSH key, to login in the Galaxy instance:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_SSHkey.png
      :scale: 30 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size. The ``Storage encryption`` option is explained here: :doc:`qs_isolate_your_galaxy`.

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_Storage1.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Storage section 1

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_Storage2.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Storage section 2

#. The Galaxy configuration section allows to select among different Galaxy versions, set the instance administrator e-mail and your Galaxy brand, select the reference dataset to attach:
   .. figure:: _static/qs_galaxy_latest/qs_galaxy_GalaxyConfig.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, bbut entering an incorrect email address will cause deployment failure.

#. Select Galaxy tools configuration and ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_Tools.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Tools section

Galaxy login
------------
The galaxy administrator password and the API key are automatically generated during the instatiation procedure and are the same for each instance:

::

  User: your user e-mail

  Password: galaxy_admin_password

  API key: ADMIN_API_KEY

.. Warning::

   The anonymous login is by default disabled.

.. Warning::

   Change Galaxy password and the API key as soon as possible!
