Get Galaxy
==========

The Galaxy section allows user to deploy a full `Galaxy production environment <https://galaxyproject.org/admin/config/performance/production-server/>`_.

The service allows to setup and launch a virtual machine configured with the Operative System CentOS 7  and the auxiliary applications needed to support a Galaxy production environment such as PostgreSQL, Nginx, uWSGI and Proftpd and to deploy the Galaxy platform itself. Once deployed each Galaxy instance can be further customized with tools and reference data.

.. seealso::

   For a detailed descreption of all Web UI options see section: :doc:`feat_galaxy_custom`.

.. seealso::

   To login into the portal see section: :doc:`feat_authentication`.

Instantiate Galaxy
------------------

#. Enter the ``Galaxy`` section:

   .. figure:: _static/qs_galaxy/qs_galaxy_FGW.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express main window

#. Set your ``Job identifier`` as you prefer, which will identfy your Galaxy in the job list, once your request is submitted:

   .. Note::

      Please be descriptive in the ``Job Identifier`` section, storing the Galaxy VM features, like user, VCPUs and Memory, tools presets and storage.

   .. figure:: _static/qs_galaxy/qs_galaxy_JobID.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Set the Number of Virtual CPUs and the Memory size:

   .. figure:: _static/qs_galaxy/qs_galaxy_VirtualHardware.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

.. Warning::

   VCPUS and Memory values selected by user have to match Image Flavor presets, otherwise a different flavor, as close as possible to the one selected, will be automatically assigned.
   Please read carefully the section: :doc:`qs_virtual_hdw_presets`.

#. Copy & Past your SSH key, to login in the Galaxy instance:

   .. figure:: _static/qs_galaxy/qs_galaxy_SSHkey.png
      :scale: 30 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size. The ``Fle system encryption`` option is explained here: :doc:`qs_isolate_your_galaxy`.

   .. figure:: _static/qs_galaxy/qs_galaxy_Storage1.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Storage section 1

   .. figure:: _static/qs_galaxy/qs_galaxy_Storage2.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Storage section 2

#. The Galaxy configuration section, allows to select different Galaxy versions, the instance administrator e-mail and set the Galaxy brand variable

   .. figure:: _static/qs_galaxy/qs_galaxy_GalaxyConfig.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, bbut entering an incorrect email address will cause deployment failure.

#. Select Galaxy tools configuration and ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy/qs_galaxy_Tools.png
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

   Change Galaxy password and the API key as soon as possible!
