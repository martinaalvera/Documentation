|galaxy_latest| configuration
=============================

Recommended images
------------------

The OS image has to be available in the Tenant. Laniakea has been tested using `CentOS 7 <https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud-1907.qcow2>`_.


CMDB configuration
------------------

The image details must be uploaded on CMDB (see section :doc:`cmdb`):

- ``image_id``: is the ID of the image on the cloud platform, e.g. Openstack.

- ``service``: is the service ID, configured on CMDB.

- ``image_name``: is the name of the image that has to be used in the tosca template in the ``image`` field.

For example, SSH on CMDb virtual machine. Then create the file ``cmdb-data/centos.json`` with the following content:

::

  {
    "type": "image",
    "data": {
        "image_id": "07e1cfd3-8f6d-4410-8ef0-c5f7eb0e09cb",
        "image_name": "centos-7-vmi",
        "architecture": "x86_64",
        "type": "linux",
        "distribution": "centos",
        "version": "7",
        "service": "service-RECAS-BARI-openstack"
    }
  }

Upload the image information on CMDB:

::

  curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/centos.json

The image shuld now be available on CMDB with the name: ``centos-7-vmi``.

.. note::

   All CMDB image are listed at the address: https://<proxy_vm_dns_name>/cmdb/image/list?include_docs=true


Tosca template configuration
----------------------------

*********
``Galxy``
*********

The TOSCA template of the |galaxy_latest| is located at ``/opt/laniakea-dashboard-config/tosca-templates/galaxy.yaml`` and is configured to exploit CentOS 7 as default image:

::

  galaxy_server:
  ...
      # Guest Operating System properties
      os:
        properties:
          image: centos-7-vmi
  ...

If the images is uploaded on CMDB with a different name, the image field needs to be changed accordingly.

**************************
``Galxy (elastic) cluser``
**************************

The |galaxy_cluster| TOSCA template is ``/opt/laniakea-dashboard-config/tosca-templates/galaxy-cluster.yaml``. The |galaxy_elastic_cluster| TOSCA template is ``/opt/laniakea-dashboard-config/tosca-templates/galaxy-elastic-cluster.yaml``.

The image configuration is the same. There are two image fields, one for the fronte node:

::

    lrms_server:
    ...
        # Front-End Guest Operating System properties
        os:
          properties:
            image: centos-7-vmi
    ...

and one for the worker node:

::

    lrms_wn:
    ...
        # Worker Node Guest Operating System properties
        os:
          properties:
            image: galaxy-base
            #image: centos-7-vmi

If the images is uploaded on CMDB with a different name, the image field needs to be changed accordingly.
