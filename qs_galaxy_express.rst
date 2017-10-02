Galaxy Express
==================

The Galaxy Express  section allows user to deploy a full `Galaxy production environment <https://galaxyproject.org/admin/config/performance/production-server/>`_.

The service loads a VM with galaxy and all tools alreadt embedded. This leads to a faster deployment, but losing some of the flexibility granted by the standard method.

In particular, it is not possible to configure Galaxy version, or retrieve last tools revision. Moreover, galaxy database password is the same for all deployments and not randomly generated.

.. Note::

   For a detailed descreption of all Web UI options see section: :doc:`feat_galaxy_custom`.

.. Note::

   To login into the portal see section: :doc:`feat_authentication`.

Instantiate Galaxy
------------------

#. Enter in the ``Galaxy express`` section:

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_FGW.png
      :scale: 80 %
      :align: center
      :alt: Galaxy express main window

#. Set your ``Job identifier`` as you prefer, which will identfy your Galaxy in the job list, once your request is submitted:

   .. figure:: _static/qs_galaxy/qs_galaxy_JobID.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Set the Number of Virtual CPUs and the Memory size:

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_VirtualHardware.png
      :scale: 25 %
      :align: center
      :alt: Virtual hardware configuration

.. Warning::

   VCPUS and Memory values selected by user have to match Image Flavor presets, otherwise a different flavor, as close as possible to the one selected, will be automatically assigned.
   Please read carefully the section: :doc:`qs_virtual_hdw_presets`.

#. Copy & Past your SSH key, to login in the Galaxy instance:

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_SSHkey.png
      :scale: 25 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size. The ``Fle system encryption`` option is explained here: :doc:`qs_isolate_your_galaxy`.

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_Storage.png
      :scale: 25 %
      :align: center
      :alt: Galaxy express Storage section

#. Set the instance administrator e-mail and the Galaxy brand variable

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_GalaxyConfig.png
     :scale: 25 %
     :align: center
     :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, bbut entering an incorrect email address will cause deployment failure.

#. Select Galaxy tools configuration:

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_Tools.png 
      :scale: 25 %
      :align: center
      :alt: Galaxy express Tools section

#. Finally, ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_submit.png
      :scale: 25 %
      :align: center
      :alt: Galaxy express submit request

   .. figure:: _static/qs_galaxy_express/qs_Gexpress_done.png
      :scale: 100 %
      :align: center
      :alt: Galaxy express deployed instance

Galaxy login
------------

The galaxy administrator password and the API key are automatically generated during the instatiation procedure and are the same for each instance:

::

  User: your user e-mail

  Password: galaxy_admin_password

  API key: ADMIN_API_KEY

.. Warning::

   Change Galaxy password and the API key as soon as possible!
