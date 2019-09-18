Identity Access Manager (IAM)
=============================

The INDIGO Identity and Access Management (IAM) is an Authentication and Authorisation Infrastructure (AAI) service which manages users credentitials and attributes, like group membership,  and authorization policies to access the resources.

VM configuration
----------------

Create VM for IAM. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Public IP address.
======= ==============================

.. warning::

   All the command will be run on the control machine.


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

Create the file ``indigopaas-deploy/ansible/application-oidc.yml``, copying and pasting the client ID, client Secret and the IAM url

::

  oidc:
  providers:
  - name: google
    issuer: https://accounts.google.com
    client:
      clientId: <iam_google_client_id>
      clientSecret: <iam_google_client_secret>
      redirectUris: https://<iam_url>/openid_connect_login
      scope: openid,profile,email,address,phone
    loginButton:
      text: Google
      style: btn-social btn-google
      image:
        fa-icon: google



Enable ELIXIR-AAI Authentication
--------------------------------

To enable you need to request a valid client ID and client Secret. Please read the corresponding `documentation <https://elixir-europe.org/services/compute/aai>`_.

Then create the file ``indigopaas-deploy/ansible/application-oidc.yml``, copying and pasting the client ID, client Secret and the IAM url:

::

  oidc:
  providers:
  - name: elixir-aai
    issuer: https://login.elixir-czech.org/oidc/
    client:
      clientId: <iam_elixiraai_client_id>
      clientSecret: <iam_elixiraai_client_secret>
      redirectUris: https://<iam_fqdn>/openid_connect_login
      scope: openid,groupNames,bona_fide_status,forwardedScopedAffiliations,email,profile
    loginButton:
      text:
      style: no-bg
      image:
        url: https://raw.githubusercontent.com/Laniakea-elixir-it/ELIXIR-AAI/master/login-button-orange.png
        size: medium


Installation
------------

In the following, both Google and ELIXIR-AAI authentication methods will be enabled. To achieve this the ``indigopaas-deploy/ansible/application-oidc.yml`` with Google and ELIXIR-AAI corresponding clients ID and clients Secret, looks like:

::

  oidc:
  providers:
  - name: google
    issuer: https://accounts.google.com
    client:
      clientId: <iam_google_client_id>
      clientSecret: <iam_google_client_secret>
      redirectUris: https://<iam_fqdn>/openid_connect_login
      scope: openid,profile,email,address,phone
    loginButton:
      text: Google
      style: btn-social btn-google
      image:
        fa-icon: google
  - name: elixir-aai
    issuer: https://login.elixir-czech.org/oidc/
    client:
      clientId: <iam_elixiraai_client_id>
      clientSecret: <iam_elixiraai_client_secret>
      redirectUris: https://<iam_fqdn>/openid_connect_login
      scope: openid,groupNames,bona_fide_status,forwardedScopedAffiliations,email,profile
    loginButton:
      text:
      style: no-bg
      image:
        url: https://raw.githubusercontent.com/Laniakea-elixir-it/ELIXIR-AAI/master/login-button-orange.png
        size: medium


Create the file ``indigopaas-deploy/ansible/inventory/group_vars/iam.yaml`` with the following configured values:

::

  iam_fqdn: <iam_vm_dns_name>
  iam_mysql_root_password: *******
  iam_organization_name: '<your_organization_name>'
  iam_logo_url: <logo_url>
  iam_account_linking_disable: true
  iam_mysql_image: "mysql:5.7"
  iam_image: indigoiam/iam-login-service:v1.5.0.rc2-SNAPSHOT-latest
  iam_notification_disable: true
  iam_notification_from: 'iam@{{iam_fqdn}}'
  iam_enable_oidc_auth: true
  iam_application_oidc_path: "/root/indigopaas-deploy/ansible/application-oidc.yml"
  iam_admin_email: '<valid_email_address>'

.. warning::

   Set also your custom mysql password with: ``iam_mysql_root_password``.

.. warning::

   Please provide a valid e-mail address, which is mandatory for Let's Encrypt certificate creation.

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible

  # ansible-playbook -i inventory/inventory playbooks/deploy-iam.yml

.. note::

   Default administrator credentials:
 
   ::

     username: admin
     password: password

.. figure:: _static/iam_login.png
   :align: center

.. centered:: Fig.2: IAM login page

Video tutorial
--------------

.. raw:: html

   <a href="https://asciinema.org/a/mh5SZHybsnAov02d3RZ757gUb" target="_blank"><img src="https://asciinema.org/a/mh5SZHybsnAov02d3RZ757gUb.svg" /></a>

IAM test
--------
Basic IAM tests.

Test 1: login as admin 
^^^^^^^^^^^^^^^^^^^^^^

#. Login as admin

   ::

      username: admin
      password: password

.. Warning:: Change default password

Test 2: Create a new user
^^^^^^^^^^^^^^^^^^^^^^^^^

#. Click Register a new account
#. Fill the form
#. Login as admin and accept the request
#. Login as new user

Test 3: Register using Google account (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Sign-in with Google 
#. Login as admin and accept the request
#. Login with Google

Create IAM Client
-----------------

#. Login as administrator or registered user.

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

#. save the client ID, client secret and client token.

.. figure:: _static/mitre.png
   :scale: 25%
   :align: center

.. centered:: Fig.3: MitreID Dashboard screenshot

 
.. figure:: _static/client_conf.png
   :scale: 25%
   :align: center

.. centered:: Fig.4: MitreID Dashboard client registration

Obtaining an IAM access token
-----------------------------

To get a vaild IAM access token, please follow this instructions:

.. toctree::
   :maxdepth: 2

   get_iam_token
