Dashboard
=========

Create IAM client for Dashboard
-------------------------------
1. Login as non-Admin user
2. Click on *MitreID Dashboard* and then *Self-service client registration*
3. Click on *New client* and compile the form wit the following paramethers


| *Client name* = dashboard

| *redirect URI* = https://<dashboard IP>/login/iam/authorized

| *scope:*

* openid
* profile
* email
* address
* phone
* offline_access

| *Grant Types*

* authorization code


| *Response types*

* code

| *credentials*

* client Secret over HTTP Post

| *Public key set*

* By URI


4. Save the client ID and client secret

5. Login as admin and from Manage Clients Re-edit the client and set also in tokens:

* Refresh tokens are issued for this client
* Refresh tokens for this client are re-used
* Active access tokens are automatically revoked when the refresh token is used
* Refresh tokens do not time out 

6. Save

Setting up dashboard role
-------------------------

Clone the `Ansible dashboard role <https://github.com/pmandreoli/ansible-dashboard-role>`_  into the control machine.

in group vars edit **dash.yaml** file with the following variable:


.. highlight:: none

::

 dash_admin_email: <email>
 dash_fqdn: <dashboard_HOSTNAME>
 dest_conf: /etc/orchestrator-dashboard
 dash_image: marica/orchestrator-dashboard:latest
 iam_client_id: ********
 iam_client_secret: ******** 
 iam_base_url: https://<IAM_HOSTNAME>
 orchestrator_url: https://<ORCHESTRATOR_HOSTNAME>
 slam_url: https://<SLAM_HOSTANAME>
 cmdb_url: https://<PROXY_HOSTANME>
 admins: <Admin_email>


.. highlight:: default

Run the role
------------

run *deploy_dash.yml* with the command `~$sudo ansible-playbook -i <inventory-path> --private-key <private_key-path> deploy-im.yml`

**deploy_dash.yml**

.. code:: yaml

   ---
   - name: Deploy dash
     hosts: dash
     become: yes
     gather_facts: false
     pre_tasks:
       - name: Check python is installed
         raw:  test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
         changed_when: false
       - name: Gathering Facts
         setup:
     roles:
       - { role: /home/ubuntu/ansible-dashboard-role }



.. figure:: _static/dashboard_homepage.png
   :scale: 50%
   :align: center

.. centered:: Orchestrator dashboard Homepage




























