SLA Manager (SLAM)
==================

SLAM IAM client creation
------------------------

1. Login in IAM as non-Admin user
2. Click on *MitreID Dashboard* and then *Self-service client registration*
3. Click on *New client* and compile the form wit the following paramethers


*Client name* = slam-client

*redirect URI* = https://<SLAM_HOSTNAME>:8443/auth

*scope:*

* openid
* profile
* email
* address
* phone
* offline_access

*Grant Types*

* authorization code

*Response types*

* code

*credentials*

* client Secret over HTTP Post

*Public key set*

* By URI

4. save the client ID and client secret

Setting up SLAM role
--------------------

1. Create and edit proxy.yaml in **group_vars** that contain all the following variables:

 .. highlight:: none

 ::
  
  letsencrypt_email: 'email'
  slam_dns_name: '<SLAM_HOSTNAME>'
  slam_mysql_password: '<password>'
  slam_mysql_root_password: '<password>'
  slam_iam_url: 'https://<IAM_HOSTNAME>'
  slam_iam_client_id: '<slam-client-ID>'
  slam_iam_client_secret: '<slam-client-secret>'
  slam_cmdb_url: 'https://<proxy_HOSTNAME>'
  slam_keystore_password: '<password>'
  slam_create_keystore: true


                   
.. highlight:: default

Run the role
------------

* Run the role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-slam.yml``

SLAM configuration
------------------

Authorize SLAM
^^^^^^^^^^^^^^

1. Go to https://<SLAM_HOSTNAME>:8443/auth it will redirect you to IAM
2. Login as admin
3. Authorize SLAM (Fig.4)

.. figure:: _static/SLAM_approvation.png
   :scale: 50%
   :align: center

.. centered:: Fig.1: SLAM authorization screenshot

.. figure:: _static/SLAM.png
   :scale: 50%
   :align: center

.. centered:: Fig.1: SLAM homepage

Negotiate resources
^^^^^^^^^^^^^^^^^^^

Resources con be negotiated trought SLAM dashboard creating new **computing and storage SLA** filling the module.

.. figure:: _static/slam_configuration.png
   :scale: 50%
   :align: center

.. centered:: Fig.2: SLAM Creating new SLA

