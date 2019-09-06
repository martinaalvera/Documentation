Infrastructure Manager (IM)
===========================

Create protected resource registration for IM
---------------------------------------------

1. Login in IAM then *MitreID Dashboard* and *Self-service protected resource registration*  
2. *New Resource*
3. Name: Infrastructure manager 
4. leave default and *Save*
5. Save *Client ID* and *Client Secret*

Setting up IM role
------------------

.. highlight:: none

::

 #group vars for reinstallation of IM version
 im_image_version: <version>
 im_mysql_root_password: ********
 im_mysql_password: *********
 im_cfg_oidc_issuers: 'https://<IAM-HOSTNAME>/'
 im_cfg_oidc_client_id: '<IM-ClientID>'
 im_cfg_oidc_client_secret: '<IM-ClientSecret>'
 im_cfg_ssh_reverse_tunnels: 'True'

.. highlight:: default

Run role
--------

command

.. code:: bash
   
 ~$ sudo ansible-playbook -i <inventory-path> --private-key <private_key-path> deploy-im.yml

IM Test
-------

.. scrivi test IM





