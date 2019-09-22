Hashicorp Vault
==================

Vault is exploited as secrets management store, to store and manage encryption passphrases

.. note::

   Current version version: 1.1.2

VM configuration
----------------

Create a VM for Vault. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Public IP address.
======= ==============================

.. warning::

   All the command will be run from the control machine VM.

IAM client configuration
-------------------------------

#. Login as admin

#. Navigate to **MitreID Dashboard** and then **Self-service client registration**

#. Click on **New client** and fill the form with the following paramethers

   ::

     Client name = dashboard_client

     redirect URI(s) = https://<dashboard_vm_dns_name>/login/iam/authorized

   .. figure:: _static/dashboard/dashboard_client_main.png
      :scale: 30%
      :align: center

#. In the Access tab select the follwing **Scopes**

   ::

     Scopes: openid, profile, email, address, phone, offline_access

   and for **Grant Types** select:

   ::

     Grant types: authorization code

   .. figure:: _static/dashboard/dashboard_client_access.png
      :scale: 30%
      :align: center

#. Save **Client ID**, **Client Secret** and **Registration Access Token**.

#. From Manage Clients Re-edit the client and set also in tokens:

   * Refresh tokens are issued for this client
   * Refresh tokens for this client are re-used
   * Active access tokens are automatically revoked when the refresh token is used
   * Refresh tokens do not time out 

6. Save

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/vault.yaml`` with the following configured values:

::

  vault_fqdn: <dashboard_vm_dns_name>
  vault_image_name: vault:1.1.2
  
  vault_iam_issuer: "https://<iam_address>/"
  vault_iam_client_id: "<im_client_id>'"
  vault_iam_client_secret: "<iam_client_secret>"
  
  vault_letsencrypt_email: "<valid_email_address>"

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-vault.yml
~                                                                                      
