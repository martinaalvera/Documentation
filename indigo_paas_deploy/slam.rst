SLA Manager (SLAM)
==================

The Service Level Agreement Manager (SLAM) role is to establish an agreement between customer and provider about capacity and quality targets. SLAM is using INDIGO IAM for authentication and INDIGO CMDB for configuration and authorization for providers.

.. note::
   Current SLAM version v2.0.0

VM configuration
----------------

Create VM for SLAM. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   1
RAM     2 GB
Network Public IP address.
======= ==============================

.. warning::

   All the command will be run from the control machine VM.

SLAM IAM client creation
------------------------

Register a new IAM client for SLAM:

#. Login in IAM as admin

#. Click on **MitreID Dashboard** and then **Self-service client registration**

#. Click on **New client** and fill the form wit the following paramethers:

   ::

     Client name:  slam_client

     redirect URI = https://<slam_vm_dns_name>:8443/auth

#. In the Access tab select the follwing **Scopes** 

   ::

     openid

     profile

     email

     address

     phone

     offline_access

    and **Grant Types**:

    ::

      authorization code

#. save the client ID and client secret.

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/slam.yaml`` with the following configured values:

 ::
  
  letsencrypt_email: '<validemail_address>'
  slam_dns_name: '<slam_dns_name>'
  slam_mysql_password: '*****'
  slam_mysql_root_password: '*****'
  slam_iam_url: 'https://<iam_dns_name>'
  slam_iam_client_id: '<slam-client-ID>'
  slam_iam_client_secret: '<slam-client-secret>'
  slam_cmdb_url: 'https://<proxy_dns_name>'
  slam_keystore_password: '*****'
  slam_create_keystore: true

.. warning::

   Set also your custom mysql password with ``slam_mysql_password``, ``lam_mysql_root_password`` and keystore password with ``slam_keystore_password``.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-slam.yml

Video tutorial
--------------

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
`
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

