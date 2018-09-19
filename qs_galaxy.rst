Get |galaxy_vm|
===============

This Galaxy  section allows user to deploy a standard `Galaxy production environment <https://galaxyproject.org/admin/config/performance/production-server/>`_.

The service instantiate a CentOS 7 Virtual Machine with Galaxy, all its companion software and tools already embedded. Once deployed each Galaxy instance can be further customized with tools and reference data.


.. seealso::

   For a detailed descreption of all Web UI options see section: :doc:`feat_options`.

.. seealso::

   To login into the portal see section: :doc:`feat_auth`.

Instantiate Galaxy
------------------

#. Enter in the ``Galaxy`` section:

   .. figure:: _static/qs_galaxy/qs_galaxy_main.png
      :scale: 28 %
      :align: center
      :alt: Galaxy express main window

#. Set your ``job identifier`` as you prefer, which will identfy your Galaxy in the job list, once your request is submitted:
   .. figure:: _static/qs_galaxy/qs_galaxy_JobID.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Set the Instance flavor, (virtual CPUs and RAM):

   .. figure:: _static/qs_galaxy/qs_galaxy_VirtualHardware.png
      :scale: 25 %
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

   .. figure:: _static/qs_galaxy/qs_galaxy_SSHkey.png
      :scale: 25 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size. The ``Storage encryption`` option is explained here: :doc:`qs_isolate_your_galaxy`.

   .. figure:: _static/qs_galaxy/qs_galaxy_Storage.png
      :scale: 25 %
      :align: center
      :alt: Galaxy express Storage section

#. Select the Galaxy version, the instance administrator e-mail, your custom Galaxy brand and the reference dataset to attach:

   .. figure:: _static/qs_galaxy/qs_galaxy_GalaxyConfig.png
     :scale: 25 %
     :align: center
     :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, but entering an incorrect email address will cause deployment failure if the ``encryption`` option is set.

#. Select Galaxy tools pre-set:

   .. figure:: _static/qs_galaxy/qs_galaxy_Tools.png 
      :scale: 25 %
      :align: center
      :alt: Galaxy express Tools section

#. Finally, ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy/qs_galaxy_submit.png
      :scale: 25 %
      :align: center
      :alt: Galaxy express submit request

   .. figure:: _static/qs_galaxy/qs_galaxy_done.png
      :scale: 100 %
      :align: center
      :alt: Galaxy express deployed instance

Galaxy login
------------
The galaxy administrator password is  automatically generated during the instatiation procedure and is the same for each deployed instance:

::

  User: your user e-mail

  Password: galaxy_admin_password

.. Warning::

   The anonymous login is by default disabled.

.. Warning::

   Change Galaxy password and the API key as soon as possible!
