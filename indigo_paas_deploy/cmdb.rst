CMDB and CPR
============

Setting up CMDB role
--------------------

1. Create and edit cmdb.yaml in **group_vars** that contain the following variables:

.. highlight:: none

::
 
 cmdb_crud_password: CMDBpassword
 cmdb_oidc_userinfo: https://<proxy_HOSTNAME>/userinfo

                   
.. highlight:: default

Run the role
------------

* Run the cmdb role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-cmdb.yml``
* Run the cpr role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-cpr.yml``

CMDB configuration
------------------
1. Login in cmdb VM
2. Create a directory called **cmdb-data**
3. Compile and move in  the following 3 .json files:

*image.json*

.. code:: json

 
  {
     "type": "image",
     "data": {
         "image_id": "",
         "image_name": "",
         "architecture": "",
         "type": "linux",
         "distribution": "ubuntu",
         "version": "16.04",
         "service": ""
     }
  }
  

*provider.json*

.. code:: json
    
   {
      "_id": "",
      "data": {
          "name": "",
          "country": "",
          "country_code": "",
          "roc": "",
          "subgrid": "",
          "giis_url": "",
          "owners": [ "" ]
      },
      "type": "provider"
   }
 

*service.json*

.. code:: json

   {
      "_id": "",
      "data": {
          "service_type": "",
          "endpoint": "",
          "provider_id": "",
          "region": "",
          "sitename": "",
          "hostname": "",
          "type": "compute"
      },
      "type": "service"
   }
     
    
    
4. Run the cmdb-add-data.sh in order to add image, provider, service, to CMDB.

*cmdb-add-data.sh*

.. code:: bash
 
   #!/bin/bash
   
   source /etc/cmdb/.cmdbenv
   
   if [[ -z "$CMDB_CRUD_USERNAME" ]]; then
   echo ENV variable CMDB_USER not set
   exit 1
   fi
   
   if [[ -z "$CMDB_CRUD_PASSWORD" ]]; then
   echo ENV variable CMDB_PASSWORD not set
   exit 1
   fi
   
   if [[ -z "$1" ]]; then
   echo "
   usage: $0 <json>
   "
   exit 1
   fi
   
   curl -X POST http://$CMDB_CRUD_USERNAME:$CMDB_CRUD_PASSWORD@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@$1

5. Control on couchDB if your configuration has been uploaded accessing it from browser.
        
.. figure:: _static/cmdb_config.png
   :scale: 50%
   :align: center

.. centered:: couchDB after configuration process, containing image, provider and service       
       
       

