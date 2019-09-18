Infrastructure Manager (IM)
===========================

The `Infrastructure Manager (IM) <https://www.grycap.upv.es>`_ is used to deploy virtual infrastructures, to deploy virtual infrastructures, e.g. Galaxy and the underlying virtual hardware.

.. note::
   Current IM version: 1.8.2

VM configuration
----------------

Create VM for IM. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Private IP address.
======= ==============================

.. warning::

   All the command will be run from the control machine VM.

IAM protected resource configuration
------------------------------------

Register a new protected resource for IM on IAM:

#. Login on IAM as admin.

#. Navigate to **MitreID Dashboard** and finally select from the left panel **Self-service protected resource registration**.

#. Create a **New Resource**.

#. Give it a name, e.g. ``infrastructure_manager``.

#. Keep the default configuration and Save.

#. Save IM **Client ID** and **Client Secret**.

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/im.yaml`` with the following configured values:

::

 im_image_version: 1.8.2
 im_mysql_root_password: ********
 im_mysql_password: *********
 im_cfg_oidc_issuers: 'https://<iam_address>/'
 im_cfg_oidc_client_id: '<im_client_id>'
 im_cfg_oidc_client_secret: '<im_client_secret>'
 im_cfg_ssh_reverse_tunnels: 'True'

.. warning::

   Set also your custom mysql password with: ``iam_mysql_root_password`` and ``im_mysql_password``.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-im.yml

Video tutorial
--------------

.. raw:: html

   <a href="https://asciinema.org/a/aliahieqrR5ab2Wc3P1ILSrIv" target="_blank"><img src="https://asciinema.org/a/aliahieqrR5ab2Wc3P1ILSrIv.svg" /></a>

IM Test
-------

.. scrivi test IM





