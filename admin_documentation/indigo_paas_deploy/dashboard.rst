Laniakea Dashboard
==================

The Laniakea Dashbaord is built on top of the INDIGO Orchestrator Dashboard.

.. note::

   Current Dahsboard version: v0.5

VM configuration
----------------

Create VM for Dashboard. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Private IP address.
======= ==============================

.. warnings::

   In this tutorial we will use the same VM for vault and the dashbord, being the two services strictly connected.

   This is not requred.

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

The Laniakea dashboard can be installed in three different ways:

#. Stateless version: this is a simple graphical User interface of the INDIGO PaaS orchestrator. The automated storage encryption will not work.

   .. toctree::
      :maxdepth: 2

      dashboard_stateless


#. With MySQL database: this version comes with a MySQL database support and requires

   .. toctree::
      :maxdepth: 2

      dashboard_db

#. With MySQL and Hashicorp Vault: this is the version exploited by default on Laniakea.

   .. toctree::
      :maxdepth: 2

      dashboard_vault
