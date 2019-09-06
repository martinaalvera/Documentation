PaaS Orchestrator
=================

Create protected resource registration for Clues
------------------------------------------------

1. Login in IAM then *MitreID Dashboard* and *Self-service protected resource registration*
2. *New Resource*

*Name: ****

*scope:*

* openid
* profile
* email
* address
* phone
* offline_access

3. Save *Client ID* and *Client Secret*
4. log out and login with Admin user
5. edit the client and set in Grant types *token exange* and introspection
6. save and exit


Create protected resource registration for Orchestrator
-------------------------------------------------------

1. Login in IAM then *MitreID Dashboard* and *Self-service protected resource registration*
2. *New Resource*

*Name: ****

*scope:*

* openid
* profile
* offline_access

3. Save *Client ID* and *Client Secret*
4. log out and login with Admin user
5. edit the client and set in Grant types *token exange* and introspection
6. save and exit


Run monitor-mock docker
-----------------------

1. Install `docker-CE <https://docs.docker.com/install/linux/docker-ce/ubuntu/>`_ on the orchestrator VM
2. run the `monitoring-mock docker <https://hub.docker.com/r/marica/monitoring-mock>`_

Setting up Orchestrator role
----------------------------


.. highlight:: none

::

 orchestrator_url: http://<PROXY_HOSTNAME>
 orchestrator_image: indigodatacloud/orchestrator:2.1.2-final
 orchestrator_mysql_root_password: ****
 orchestrator_mysql_password: ****
 orchestrator_im_url: http://<PROXY_HOSTNAME>:8800
 orchestrator_cmdb_url: http://<PROXY_HOSTNAME>/cmdb
 orchestrator_slam_url: https://<SLAM_HOSTNAME>:8443/rest/slam
 orchestrator_cpr_url: http://<PROXY_HOSTNAME>:80
 orchestrator_monitoring_url: http://localhost:8082
 orchestrator_iam_issuer: https://<IAM_HOSTNAME>/
 orchestrator_iam_client_id: <ORCHESTRATOR_CLIENT_ID>
 orchestrator_iam_client_secret: <ORCHESTRATOR_CLIENT_SECRET>
 orchestrator_clues_iam_client_id: <CLUES_CLIENT_ID> 
 orchestrator_clues_iam_client_secret: <CLUES_CLIENT_SECRET> 
 orchestrator_custom_types: https://raw.githubusercontent.com/mtangaro/tosca-types/master/custom_types.yaml
 

.. highlight:: default

Run the role
------------

* run the role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-slam.yml``

