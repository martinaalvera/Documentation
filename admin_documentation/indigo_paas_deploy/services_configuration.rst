The last mile: applications configuration
=========================================

By default, Laniakea is configured to run the following applications:

---------------------
``Galaxy Live Build``
---------------------

:Description:
	The Galaxy live build allows to setup and launch a virtual machine configured with the Operative System CentOS 7 and the auxiliary applications needed to support a Galaxy production environment such as PostgreSQL, Nginx, uWSGI and Proftpd and to deploy the Galaxy platform itself and the tools that come with the selected flavour.

	This application can be deployed with cluster support, using SLURM as Resource Manager and with automatica elasticity support, with CLUES as elasticity manager.

:Recommended images:
	`CentOS-7-x86_64-GenericCloud-1907.qcow2 <https://cloud.centos.org/centos/7/images>`_

:Configuration:
	:doc:`galaxy_latest`

------------------
``Galaxy Express``
------------------

:Description:
	The Galaxy express instantiate a CentOS 7 Virtual Machine with Galaxy, all its companion software and the set of tools that come with the selected flavour. Once deployed each Galaxy instance can be further customized with additional tools and reference data.

	This application can be deployed with cluster support, using SLURM as Resource Manager.

:Configuration:
        :doc:`galaxy_vm`

-----------------
``Galaxy Docker``
-----------------

:Description:
	The Galaxy Docker instantiate an Ubuntu 16.04 Virtual Machine with the Galaxy official Docker. Once deployed each Galaxy instance can be further customized with additional tools and reference data.

:Recommended images:
	`Ubuntu 16.04 LTS cloud images <https://cloud-images.ubuntu.com/xenial/>`_

:Configuration:
        :doc:`galaxy_docker`

---------------------
``Test applications``
---------------------

:Description:
	Two test recipes are shipped by default to test a simple Ubuntu or Centos deployment with or without storage volume

:Recommended images:
        `CentOS-7-x86_64-GenericCloud-1907.qcow2 <https://cloud.centos.org/centos/7/images>`_ or `Ubuntu 16.04 LTS cloud images <https://cloud-images.ubuntu.com/xenial/>`_


:Configuration:
        :doc:`test_deployments`
