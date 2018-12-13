Get |galaxy_cluster|
====================

.. Warning::

   Currently, this feature is under beta testing. Galaxy and tools are installed on-the-fly starting from a bare CentOS 7 image. The whole process, i.e. install Galaxy and tools, may take time. We will soon add the possibility to exploit images with tools to speed-up the configuration.

It is possible to deploy a Galaxy cluster, using SLURM as Resource Manager, with or without automatic elasticity support.

#. Galaxy cluster section: all working nodes are deployed with the Galaxy server and are always available. 

#. Galaxy elastic cluster serciont: automatic elasticity enables dynamic cluster resources scaling, deploying and powering on new working nodes depending on the workload of the cluster and powering-off them when no longer needed. This provides an efficient use of the resources, making them available only when really needed.

The two sections provide the same configuration options. 

.. Warning::

   Each node takes 12 minutes or more to be instantiated. Therefore, the job needs the same time to start. On the contrary if the node is already deployed the job will start immediately.

.. seealso::

   For a detailed description Galaxy elastic cluster see section :doc:`feat_cluster_support`.

   For a detailed descreption of all Web UI options see section: :doc:`feat_options`.

   To login into the portal see section: :doc:`feat_auth`.


Instantiate Galaxy
------------------

#. Enter in the ``Galaxy cluster`` section:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_main.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express main window

#. Describe your instance using the ``Instance description`` field, which will identfy your Galaxy in the job list, once your request is submitted.

#. Select the number of Virtual Worker Nondes of your Cluster:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Vhw1.png
      :scale: 100 %
      :align: center
      :alt: Virtual hardware configuration

#. Select the Instance flavor, (virtual CPUs and RAM) for your Front node, i.e. the Galaxy server, and for each Worker Node:

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

#. Copy & Paste your SSH key, to login in the Galaxy instance:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_SSHkey.png
      :scale: 100 %
      :align: center
      :alt: SSH public key injection

#. Storage section allows to select the IaaS storage volume size. The ``Storage encryption`` option is explained here: :doc:`qs_encryption`.

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Storage.png
      :scale: 100 %
      :align: center
      :alt: Galaxy express Storage section 2

#. Select the Galaxy version, the instance administrator e-mail and your custom Galaxy brand:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_GalaxyConfig.png
     :scale: 100 %
     :align: center
     :alt: Galaxy express Galxy configuration section

  .. Warning::

     Please insert a vail mail address. No check is performed on its syntax, but entering an incorrect email address will cause deployment failure if the ``encryption`` option is set.

#. Select Galaxy tools pre-set:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_Tools.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express Tools section

#. and reference dataset:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_refdata.png 
      :scale: 100 %
      :align: center
      :alt: Galaxy express Tools section

#. Finally, ``SUBMIT`` your request:

   .. figure:: _static/qs_galaxy_cluster/qs_cluster_view.png
      :scale: 100 %
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
