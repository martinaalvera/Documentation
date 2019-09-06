Identity Access Manager (IAM)
=============================

The INDIGO Identity and Access Management (IAM) is an Authentication and Authorisation Infrastructure (AAI) service which manages users credentitials and attributes, like group membership,  and authorization policies to access the resources.

VM configuration
----------------

Create an Ubuntu 16.04 VM with at least 2 vCPUs, 4 GB of RAM and a public IP address and set the SSH public key to allow Ansible to connect to the remote VM.

.. warning::

   All the command will be run on the ``master`` VM.


Enable Google Authentication
----------------------------

To enable Google authentication access to `Google developers console <https://console.developers.google.com/apis/credentials>`_ and create and configure a new credential project.

#. Create Credentials > OAuth Client ID

#. Application Type: Web Application

#. Name: Set a custom Service Provider (SP) name

#. Authorized JavaScript origins: https://<iam_vm_dns_name>.

#. Authorized redirect URIs: https://<iam_vm_dns_name>/openid_connect_login

#. Create the client

#. Copy your client ID and client secret

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/iam.yaml`` with the following configured values:

::

  iam_fqdn: <iam_vm_dns_name>
  iam_mysql_root_password: *******
  iam_organization_name: '<your_organization_name>'
  iam_logo_url: <logo_url>
  iam_enable_google_auth: true
  iam_account_linking_disable: true
  iam_mysql_image: "mysql:5.5"
  iam_image: indigoiam/iam-login-service:v1.4.0-latest
  iam_notification_disable: true
  iam_notification_from: 'iam@{{iam_fqdn}}'
  iam_google_client_id: '<google_client_ID>'
  iam_google_client_secret: '<google_client_secret>'
  iam_admin_email: '<valid_email_address>'

.. warning::

   Set also your custom mysql password with: ``iam_mysql_root_password``.

.. warning::

   Please provide a valid e-mail address, which is mandatory for Let's Encrypt certificate creation.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible

  # ansible-playbook -i inventory/inventory playbooks/deploy-iam.yml

.. figure:: _static/iam_login.png
   :scale: 25%
   :align: center

.. centered:: Fig.2: IAM login page

Video tutorial
--------------

.. raw:: html

   <script id="asciicast-266305" src="https://asciinema.org/a/266305.js" async></script>

IAM test
--------
Basic IAM tests.

Test 1: login as admin 
^^^^^^^^^^^^^^^^^^^^^^

#. Login as admin

   ::

      username: admin
      password: password

#. Change default password

Test 2: Create a new user
^^^^^^^^^^^^^^^^^^^^^^^^^

#. Click Register a new account
#. Fill the form
#. Login as admin and accept the request
#. Login as new user

Test 3: register using Google account (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Sign-in with Google 
#. Login as admin and accept the request
#. Login with Google

Create IAM Client
-----------------

#. Login as user, i.e. non Administrator user
#. Click on *MitreID Dashboard* and then *Self-service client registration*
#. Click on *New client* and compile the form wit the following parameters

   ::

     Client name = iam-client-name

     redirect URI = https://<service_hostname>

#. Configure your client, for example:

   ::

     scope:
       * openid
       * profile
       * email
       * address
       * phone
       * offline_access
       
     Grant Types
       
       * authorization code
       * refresh

#. save the client IDm, client secret and client token.

.. figure:: _static/mitre.png
   :scale: 25%
   :align: center

.. centered:: Fig.3: MitreID Dashboard screenshot

 
.. figure:: _static/client_conf.png
   :scale: 25%
   :align: center

.. centered:: Fig.4: MitreID Dashboard client registration
