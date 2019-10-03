Install Laniakea dashboard (database and vault version)
=======================================================

.. Warning::

   Vault integration leverages on MySQL database. It can't work with dashboard stateless version

IAM client configuration
-------------------------------


#. Navigate to **MitreID Dashboard** and then **Self-service client registration**

#. Login on IAM then **MitreID Dashboard** and select **Self-service client registration** as Administrator user.

#. Click on **New client** and fill the form with the following paramethers

   ::

     Client name = dashboard_client

     redirect URI(s) = https://<dashboard_vm_dns_name>/login/iam/authorized

   .. figure:: _static/vault/vault_client_main.png
      :scale: 30%
      :align: center

#. In the Access tab select the follwing **Scopes**

   ::

     Scopes: openid, profile, email, address, phone, offline_access

   and for **Grant Types** select:

   ::

     Grant types: authorization code

   .. figure:: _static/vault/vault_client_access.png
      :scale: 30%
      :align: center

#. Save the client.

#. Save **Client ID**, **Client Secret** and **Registration Access Token** or the full output json in the **JSON** tab for future access.

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/orchestrator-dashboard.yaml`` with the following configured values:

::

  dashboard_fqdn: <dashboard_vm_dns_name>
  dashboard_image_name: laniakeacloud/laniakea-dashboard:stable
  
  dashboard_iam_issuer: "https://<iam_address>/"
  dashboard_iam_client_id: "<im_client_id>'"
  dashboard_iam_client_secret: "<iam_client_secret>"
  dashboard_orchestrator_url: "https://<proxy_vm_dns_name>/orchestrator"
  
  dashboard_tosca_template_repository_url: https://github.com/Laniakea-elixir-it/laniakea-dashboard-config.git
  dashboard_tosca_template_repository_dir: "/opt/laniakea-dashboard-config"
  dashboard_tosca_templates_dir: "/opt/laniakea-dashboard-config/tosca-templates"
  dashboard_tosca_parameters_dir: "/opt/laniakea-dashboard-config/tosca-parameters"
  dashboard_tosca_metadata_dir: "/opt/laniakea-dashboard-config/tosca-metadata"
  dashboard_slam_url: "https://<slam_vm_dns_name>:8443"
  dashboard_cmdb_url: "https://<proxy_vm_dns_name>/cmdb"
  dashboard_administrators: "['<valid_email_address>']"
  
  dashboard_letsencrypt_email: "<valid_email_address>"

  dashboard_enable_db: True
  dashboard_db_sql_file_url: "https://raw.githubusercontent.com/Laniakea-elixir-it/orchestrator-dashboard/laniakea-stable/utils/orchestrator_dashboard.sql"
  dashboard_mysql_root_password: *****
  dashboard_db_password: ******

  dashboard_enable_vault: True
  dashboard_vault_token: "<vault_valid_token>"
  dashboard_vault_iam_client_id: "vault_iam_client_id>"
  dashboard_vault_iam_client_secret: "<vault_iam_client_secret"


.. warning::

   Set also your custom mysql password with: ``dashboard_mysql_root_password`` and ``dashboard_mysql_password``.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-orchestrator-dashboard.yml


Video Tutorial
--------------
