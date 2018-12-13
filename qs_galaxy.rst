Get |galaxy_latest| 
===================

The Galaxy section allows user to deploy a full `Galaxy production environment <https://docs.galaxyproject.org/en/latest/admin/production.html>`_.

The service allows to setup and launch a virtual machine configured with the Operative System CentOS 7 and the auxiliary applications needed to support a Galaxy production environment such as PostgreSQL, Nginx, uWSGI and Proftpd and to deploy the Galaxy platform itself and the selected Galaxt tools.

.. Warning::

   Everything is configured on the fly and, depending on the number of the tools to be installed may take time.

.. seealso::

   For a detailed descreption of all Web UI options see section: :doc:`feat_options`.

.. seealso::

   To login into the portal see section: :doc:`feat_auth`.

Instantiate Galaxy
------------------

#. Enter the |galaxy_latest| section:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_main.png 
      :scale: 70 %
      :align: center
      :alt: Galaxy express main window

#. Describe your instance using the ``Instance description`` field, which will identfy your Galaxy in the job list, once your request is submitted.

#. Select your instance flavour (virtual CPUs and the memory size):

   Currently, the following pre-sets are available, but not all of them are enabled.

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
      :scale: 50 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the user storage volume size. The ``Enable encryption`` flag is explained here: :doc:`qs_encryption`.

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_Storage.png
      :scale: 50 %
      :align: center
      :alt: Galaxy express Storage section

#. Select the Galaxy version, the instance administrator e-mail, your custom Galaxy brand and the reference dataset to attach:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_GalaxyConfig.png
     :scale: 50 %
     :align: center
     :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, but entering an incorrect email address will cause deployment failure if the ``encryption`` option is set.

#. Select Galaxy tools pre-set:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_Tools.png 
      :scale: 50 %
      :align: center
      :alt: Galaxy express Tools section

#. and reference dataset:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_refdata.png 
      :scale: 50 %
      :align: center
      :alt: Galaxy express Tools section

#. Finally, ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy_latest/qs_galaxy_view.png
      :scale: 80 %
      :align: center
      :alt: Galaxy express submit request

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
