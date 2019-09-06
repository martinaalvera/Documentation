Laniakea deployment
===================

Laniakea relies on the INDIGO-DataCloud `software catalogue <https://www.indigo-datacloud.eu/electricindigo-software-catalogue>`_. The Fig. 1 shows the deployment strategy to be followed to install Laniakea.

.. figure:: _static/paas_deploy.png
   :scale: 80%
   :align: center

.. centered:: Fig.1: PaaS component architecture scheme

We tested our deployment on OpenStack `Mitaka <https://releases.openstack.org/mitaka/index.html>`_ and `Stein <https://releases.openstack.org/stein/index.html>`_, using Ubuntu 16.04 as default OS.

Each INDIGO component is installed using its official Docker container and run on a specific Virtual Machine.

Tab. 1 shows the VMs tha has to be created, their requirements and the corresponding ports configuration needed to install Laniakea.

Please create the needed VMs with the following configuration:

+----------------------------------------------+------+------+-----------------------+---------------+
| INDIGO Component                             | RAM  | vCPU | Ports                 | Network       |
+==============================================+======+======+=======================+===============+
| Proxy server                                 | 2 GB | 1    | 443, 8080             | | public IP   |
|                                              |      |      |                       | | private IP  |
+----------------------------------------------+------+------+-----------------------+---------------+
| Identity and Access Manager (IAM)            | 4 GB | 2    | 443                   | public IP     |
+----------------------------------------------+------+------+-----------------------+---------------+
| Infrastructure Manager (IM)                  | 4 GB | 2    | 8800                  | private IP    |
+----------------------------------------------+------+------+-----------------------+---------------+
| | Change Management Database (CMDB),         | 4 GB | 2    | 443, 5984, 8080, 8081 | private IP    |
| | Cloud Provider Ranker (CPR)                |      |      |                       |               |
+----------------------------------------------+------+------+-----------------------+---------------+
| Service Level Agreement Manager (SLAM)       | 2 GB | 1    | 8443, 443             | public IP     |
+----------------------------------------------+------+------+-----------------------+---------------+
| PaaS Orchestrator                            | 4 GB | 2    | 443                   | private IP    |
+----------------------------------------------+------+------+-----------------------+---------------+
| HashiCorp Vault and Dashboard                | 4 GB | 2    | 443                   | public IP     |
+----------------------------------------------+------+------+-----------------------+---------------+

In particular we highlight in the table the VM Network configuration, i.e. if the VM needs a public IP address to be accessed from outside or a private IP address is enough.

Once installed the services will be available at the following endpoint:

Services end-points
-------------------
.. csv-table:: **Services end-points**
   :header: "Service", "end-point"
   :widths: auto
   :file: ./end_point.csv
