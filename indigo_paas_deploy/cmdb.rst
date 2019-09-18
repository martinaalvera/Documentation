CMDB and CPR
============

The Configuration Management DataBase (CMDB) is used to contain all the configuration items (CIs) that are valid to manage the infrastructure.

The Cloud Provider Ranker is a standalone REST WEB Service which ranks cloud providers.

CMDB and CPR are installed on the same machine.

VM configuration
----------------

Create VM for CMDB and CPR. The VM should meet the following minimum requirements:

======= ==============================
OS      Ubuntu 16.04
vCPUs   2
RAM     4 GB
Network Private IP address.
======= ==============================

.. warning::

   All the command will be run from the control machine VM.

CMDB installation
-----------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/cmdb.yaml`` with the following configured values:

::
 
 cmdb_crud_password: *****
 cmdb_oidc_userinfo: https://<proxy_url>/userinfo

Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-cmdb.yml

CMDB video tutorial
-------------------

.. raw:: html

   <a href="https://asciinema.org/a/nDH95eYYJ5twW7fi6B5tsc7WB" target="_blank"><img src="https://asciinema.org/a/nDH95eYYJ5twW7fi6B5tsc7WB.svg" /></a>

CMDB configuration
------------------

The current version of CMDB is supporting set of configuration elements that are vital for INDIGO operations:

- providers: organizational entity that owns or operates the services;

- services (both computing and storage): main technical component description defining type and location of technical endpoints;

- images: local service metadata about mapping of INDIGO-wide names of images, which are necessary to translate TOSCA description into service specific request.

CMDB needs to be populated with IaaS provider, services and images information.

In the following we will

#. SSH on cmdb virtual machine.

#. Create a directory called **cmdb-data**

   ::

     # mkdir cmdb-data

#. Create the file ``cmdb-data/provider.json``

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

#. Create the file ``cmdb-data/service.json``

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

#. Create the file ``cmdb-data/image.json``

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

   where the ``ìmage_id`` is the image ID on the Cloud Provider Manager, e.g. OpenStack.
 
#. Add providers, services and images to CMDB.

   Create the file ``cmdb-add-data.sh`` with the content:

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

   give it execution permissions:

   ::

     chmod +x cmdb-add-data.sh

   Finally you can upload informations to cmdb using curl:

   ::

     curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/provider.json

     curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/service.json

     curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/image.json

#. Check on CMDB couchDB if your configuration has been uploaded from your browser at the following endpoint: ``https://<proxy_url>/couch/_utils/database.html?indigo-cmdb-v2``
        
.. figure:: _static/cmdb_config.png
   :scale: 50%
   :align: center

.. centered:: CMDB couchDB after the configuration process with provider, service and image. 
       
CPR installation
----------------

CPR does not need any configuration. Run the role using the ``ansible-playbook`` command:

::

  # cd indigopaas-deploy/ansible 

  # ansible-playbook -i inventory/inventory playbooks/deploy-cpr.yml

CPR video tutorial
------------------

.. raw:: html

   <a href="https://asciinema.org/a/Hxbupwdk3DCzSSCR6LB37dBxq" target="_blank"><img src="https://asciinema.org/a/Hxbupwdk3DCzSSCR6LB37dBxq.svg" /></a>
