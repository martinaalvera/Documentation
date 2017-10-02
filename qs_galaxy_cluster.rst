Galaxy elastic cluster (SLURM)
==============================

The Galaxy elastic cluster section allow user to deploy Galaxy and a SLURM cluster with automatic elasticity.

This enables dynamic cluster resources scaling, deploying and powering on new working nodes depending on the workload of the cluster and powering-off them when no longer needed. This provides an efficient use of the resources, making them available only when really needed.

.. Note::

   For a detailed description Galaxy elastic cluster see section :doc:`feat_cluster_support`.

.. Note::

   For a detailed descreption of all Web UI options see section: :doc:`feat_galaxy_custom`.

.. Note::

   To login into the portal see section: :doc:`feat_authentication`.

Instantiate Galaxy
------------------

#. Enter the ``Galaxy elastic cluster`` section:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_FGW.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express main window

#. Set your ``Job identifier`` as you prefer, which will identfy your Galaxy in the job list, once your request is submitted:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_JobID.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Set the number of Virtual Worker Nondes of your Cluster:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Vhw1.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

#. Set the Number of Virtual CPUs and the Memory size for your Front node (i.e. the Galaxy server) and each Worker Node:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Vhw2.png
      :scale: 30 %
      :align: center
      :alt: Virtual hardware configuration

.. Warning::

   VCPUS and Memory values selected by user have to match Image Flavor presets, otherwise a different flavor, as close as possible to the one selected, will be automatically assigned.
   Please read carefully the section: :doc:`qs_virtual_hdw_presets`.

#. Copy & Past your SSH key, to login in the Galaxy instance:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_SSHkey.png
      :scale: 30 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size.

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Storage.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Storage section 2

#. The Galaxy configuration section, allows to select different Galaxy versions, the instance administrator e-mail and set the Galaxy brand variable

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_GalaxyConfig.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, bbut entering an incorrect email address will cause deployment failure.

#. Select Galaxy tools configuration and ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Tools.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Tools section

#. Once the job is in ``DONE`` state, the galaxy server address is available and Galaxy is ready.

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_DONE.png
      :scale: 30 %
      :align: center
      :alt: Galaxy express Tools section

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Galaxy.png
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
