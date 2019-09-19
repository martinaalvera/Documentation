PaaS Orchestrator
==================

PaaS Orchestrator is  the  core  component  of  the  PaaS  layer.  It  collects  high-level deployment requests from the software layer, and coordinates the resource or service deployment.

.. note::
   Current Orchestrator version: 2.1.2-final

VM configuration
----------------

Create VM for IM. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Private IP address.
======= ==============================

IAM  protected resource configuration for CLUES
------------------------------------------------

#. Login on IAM then **MitreID Dashboard** and select a **Self-service protected resource registration** as Administrator user.

#. Select *New Resource* with the follwoing parameters

   ::

     Name: clues_client

     Scopes: openid, profile, email, address,  phone, offline_access

     Grant Types: token exchange

   and check the flag at **Introspection**:

   ::

     Introspection Allow calls to the Introspection Endpoint?

#. Save **client ID** and **client secret**

.. Warning::

   If you did not create this resource ad aministrator user you will not be able to enable the **token exchange** grant type and introspection. To fix this: log out and login as Admin user and edit the client, setting in Grant types **token exange** and flagging **introspection**.

IAM protected resource configuration for the Orchestrator
---------------------------------------------------------

#. Login on IAM then **MitreID Dashboard** and select a **Self-service protected resource registration** as Administrator user.

#. Select *New Resource* with the follwoing parameters

   ::

     Name: orchestrator_client

     Scopes: openid, profile, offline_access

   and check the flag at **Introspection**:

   ::

     Introspection Allow calls to the Introspection Endpoint?

#. Save **client ID** and **client secret**

.. Warning::

   If you did not create this resource ad aministrator user you will not be able to enable the **token exchange** grant type and introspection. To fix this: log out and login as Admin user and edit the client, setting in Grant types **token exange** and flagging **introspection**.

Monitoring-mock installation
----------------------------

In this guide we avoid monitoring installation, leaving this job to the Cloud provider.

To do this SSH on the orchestrator VM and run the monitoring-mock docker:

::

  docker run -d --restart always --name monitoring-mock -p 8082:8082 marica/monitoring-mock:latest

.. Warning::

   This command has to be run directly on the Orchestrator VM, not on the control machine.

Orchestrator Installation
----------------------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/orchestrator.yaml`` with the following configured values:

::

  orchestrator_url: https://<proxy_dns_name>/orchestrator
  orchestrator_image: indigodatacloud/orchestrator:2.1.2-final
  orchestrator_mysql_root_password: *****
  orchestrator_mysql_password: *****
  orchestrator_im_url: https://<proxy_dns_name>/im
  orchestrator_cmdb_url: http://<proxy_dns_name>/cmdb
  orchestrator_slam_url: https://<slam_dns_name>:8443/rest/slam
  orchestrator_cpr_url: http://<proxy_dns_name>:80
  orchestrator_monitoring_url: http://localhost:8082
  orchestrator_iam_issuer: https://<iam_dns_name>/
  orchestrator_iam_client_id: <orchestrator_client_id>
  orchestrator_iam_client_secret: <orchestrator_client_secret>
  orchestrator_clues_iam_client_id: <clues_client_id> 
  orchestrator_clues_iam_client_secret: <clues_client_secrett> 
  orchestrator_custom_types: https://raw.githubusercontent.com/mtangaro/tosca-types/master/custom_types.yaml
 

.. Warning::

   SLAM and IAM are the only two services requiring a public IP, on the contrary all the others are behind the proxy.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-orchestrator.yml

Video tutorial
--------------
