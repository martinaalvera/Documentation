Cluster support (SLURM)
=======================

The service provides support for virtual clusters through a dedicated section of the web front-end and allows to instantiate Galaxy with SLURM (slurm.schedmd.com) as Resource Manager and to customize the number of virtual nodes, nodes and master virtual hardware.

Automatic elasticity, provided using the CLUES INDIGO service component (:doc:`indigo_clues`), enables dynamic cluster resources scaling, deploying and powering on new working nodes depending on the workload of the cluster and powering-off them when no longer needed. This provides an efficient use of the resources, making them available only when really needed.

Each node is configured according to the Galaxy tools installed on the VM as selected by the user during the configuration phase. All tools pre-set are tested to work with the galaxy elastic cluster.

Conda packages used to solve Galaxy tools dependencies are stored in ``/export/_conda`` directory and shared between front and worker nodes. This

The service is scalable and both users and service providers can chose among a full range of different computational capabilities: from limited ones to serve e.g. small research groups, Galaxy developers or for didactic and training purposes, to instances with elasticity cluster support to deliver enough computational power for any kind of bioinformatic analysis and number of users, opening the route for the migration of public Galaxy instances to this service.

Shared file system
------------------
Current cluster configuration foresee two path shared between front and worker nodes: 

#. ``/home`` where galaxy is installed.

#. ``/export`` where galaxy input and output datasets are hosted.

.. Note::

   NFS exports configuration file: ``/etc/exports``

Nodes deployment
----------------

.. Warning::

   Worker node deployment takes 10 minutes! Then your job will run.
   If the node is already deployed the job starts immediately.

This is due to: 

#. VM configuration

#. Tools dependencies installation

#. CernVM-FS configuration

#. SLURM installation and configuration

SLURM main commands
-------------------
Please have a look here for a summary of SLURM main commands:
https://www.rc.fas.harvard.edu/resources/documentation/convenient-slurm-commands/
