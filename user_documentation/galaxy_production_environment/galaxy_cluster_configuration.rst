Cluster configuration
======================

|project_name| provides the possibility to instantiate Galaxy with `SLURM <slurm.schedmd.com>`_ as Resource Manager and to customize the number of virtual workern nodes and the workenr nodes and front-end server virtual hardware, e.g. vCPUs and memory.

Furthermore, automatic elasticity, provided using the `CLUES <https://ec3.readthedocs.io/en/latest/arch.html#clues>`_, enables dynamic cluster resources scaling, deploying and powering on new working nodes depending on the workload of the cluster and powering-off them when no longer needed. This provides an efficient use of the resources, making them available only when really needed.

Conda packages used to solve Galaxy tools dependencies are stored in ``/export/tool_deps/_conda`` directory and shared between front and worker nodes.

Shared file system
------------------
Current cluster configuration foresee two path shared between front and worker nodes: 

#. ``/home`` where Galaxy is installed.

#. ``/export`` where Galaxy input and output datasets are stored.

.. Note::

   NFS exports configuration file: ``/etc/exports``

Nodes deployment
----------------

.. Warning::

   Each node takes 12 minutes or more to be instantiated. Therefore, the job needs the same time to start. On the contrary, if the node is already deployed, the job will start immediately.

This is due to: 

#. Virtual Machine configuration

#. CernVM-FS configuration

#. SLURM installation and configuration

SLURM main commands
-------------------

`Connecting Galaxy to a compute cluster <https://galaxyproject.github.io/training-material/topics/admin/tutorials/connect-to-compute-cluster/tutorial.html>`_

`SLURM main commands <https://www.rc.fas.harvard.edu/resources/documentation/convenient-slurm-commands/>`_

`Sbatch commands <https://slurm.schedmd.com/sbatch.html>`_
