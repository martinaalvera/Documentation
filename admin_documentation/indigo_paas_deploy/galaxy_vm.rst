|galaxy_vm| configuration
=========================

|galaxy_vm| exploits custom images with Galaxy, all its companion software and tools inside it. In particular, tools are installed on Galaxy but their dependencies are not included in the image, otherwise its size would make deployment slow and difficult to manage. For this reason the ``tool_deps`` directory is compressed in a separated tarball, which is downloaded and extracted at the deployment time.

Image creation
--------------

Galaxy flavours images can be created using Laniakea ansible roles:

- :doc:`/admin_documentation/ansible/ansible_galaxycloud`
- :doc:`/admin_documentation/ansible/ansible_galaxycloud-tools`

A setup script is available to automate the procedure `here <https://github.com/Laniakea-elixir-it/laniakea-images>`_.
The setup script can used to create Laniakea cloud images. It is compatible with CentOS 7 and Ubuntu 16.04. CentOS 7 is the recommended OS.
This script update all CentOS or Ubuntu image packages. CVMFS client is installed by default. Other installed packages: vim, wget, git.
On CentOS 7 epel repository are enabled by default.

The script can be also used to create a tar.gz with conda tools dependencies on /export path. The created tarball will have the galaxy flavour name.

Image upload
------------

Once create the Galaxy image has to be made available in the cloud provider tenant. For example, on Openstack:


mettere l'immagine di openstack


Tools upload
------------

The tarrball with the tools must be available to be downloaded at deployment time. Laniakea tarball are currently available (with the corresponding cloud images) here:

http://cloud.recas.ba.infn.it:8080/v1/AUTH_3b4918e0a982493e8c3ebcc43586a2a8/Laniakea-generic-cloud-images

The :doc:`/admin_documentation/ansible/ansible_galaxycloud-fastconfig` ansible role, download and uncompress the tools dependencies in the right path. A naming convention has been adoped to grant the donwload of the tarball file, corresponding to the right cloud image: <galaxy_flavour>-<galaxy_version>-<image_version>. For example ``galaxy-rna-workbench-release_19.05-1``.

- <galaxy_flavour>: it is the selected Galaxy flavour, e.g. ``galaxy-CoVaCS``.
- <galaxy_version>: it is the selected Galaxy version, e.g. ``release_19.05``.
- <image_version>:  it is the version of the cloud image, currently available. For each Galaxy flavour and Galaxy version, the image version can be checked `here <https://github.com/indigo-dc/ansible-role-galaxycloud-fastconfig/tree/master/vars>`_. For example, the image version of ``galaxy-CoVaCS`` for each Galaxy release can be found `here <https://raw.githubusercontent.com/indigo-dc/ansible-role-galaxycloud-fastconfig/master/vars/galaxy-CoVaCS.yml>`_.

CMDB configuration
------------------

|galaxy_vm| exploits custom images with Galaxy already inside. Therefore, a naming convention is used, allowing the TOSCA template to call the right image: ``centos-7-<galaxy_flavour>-<galaxy_version>``, where ``<galaxy_flavour≤`` is the selected flavour and ``<galaxy_version`` ins the selected Galaxy version.

Therefore, the image name uploaded on CMDB must follow this convention. For example, if the ``galaxy_flavour = galaxy-CoVaCS`` and the ``galaxy_version = release_19.05`` the resultant image name will be ``centos-7-galaxy-CoVaCS-release_19.05``.

The follwing naming convenction is used in Laniakea:

================================== =================================  ========================================================================================================================================================================
Flavours                           Name                               Description
================================== =================================  ========================================================================================================================================================================
Galaxy minimal                     galaxy-no-tools                    Galaxy production-grade server (Galaxy, PostgreSQL, NGINX, proFTPd, uWSGI).
Galaxy CoVaCS                      galaxy-CoVaCS                      Workflow for genotyping and variant annotation of whole genome/exome and target-gene sequencing data (https://www.ncbi.nlm.nih.gov/pubmed/29402227).
Galaxy GDC Somatic Variant         galaxy-GDC_Somatic_Variant         Port of the Genomic Data Commons (GDC) pipeline for the identification of somatic variants on whole exome/genome sequencing data (https://gdc.cancer.gov/node/246).
Galaxy RNA workbench               galaxy-rna-workbench               More than 50 tools for RNA centric analysis (https://www.ncbi.nlm.nih.gov/pubmed/28582575).
Galaxy Epigen                      galaxy-epigen                      Based on Epigen project (http://www.epigen.it/).
================================== =================================  ========================================================================================================================================================================

TOSCA template configuration
----------------------------

The |galaxy_vm| TOSCA template needs to be configured to use the right image and download the right tool tarball.

Tools tarball repository is set in the ``inputs`` section of the TOSCA template:

::

  remote_tool_deps_dir_url:
    type: string
    description: tools tar gz location
    default: 'http://cloud.recas.ba.infn.it:8080/v1/AUTH_3b4918e0a982493e8c3ebcc43586a2a8/Laniakea-generic-cloud-images'

The image can be configured in the section ``galaxy_server``, with the image inserted in CMDB, allowing the PaaS Orchestrator to retrieve the right image:

::

  galaxy_server:
  ...
      # Guest Operating System properties
      os:
        properties:
          image: { concat: ['centos-7-', get_input: flavor,'-', get_input: version ] } # centos-7-galaxy-CoVaCS-release_19.05
  ...

The image prefix ``centos-7`` is arbitrary and can be modified, but it must be the same on the CMDB image name and the TOSCA template.

galaxy-minimal
--------------

***************
``Description``
***************
Galaxy production-grade server (Galaxy, PostgreSQL, NGINX, proFTPd, uWSGI).

*********
``Image``
*********

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-minimal_release_19.05-1.qcow2

*************
``CMDB json``
*************

Create the file ``cmdb-data/galaxy-minimal.json`` on the CMDB Virtual Machine, with the content:

::

  {
    "type": "image",
    "data": {
        "image_id": "<galaxy-minimal-image-id>",
        "image_name": "centos-7-galaxy-minimal-release_19.05",
        "architecture": "x86_64",
        "type": "linux",
        "distribution": "centos",
        "version": "7",
        "service": "<service-id>"
    }
  }

where ``galaxy-minimal-image-id`` is the image ID on the Cloud platform, while ``service-id`` is the service ID on CMDB.

***********************
``CMDB upload command``
***********************

On CMDB Virtual Machine run the following command:

::

  curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/galaxy-minimal.json

where ``<cmdb_crud_password>`` is the CMDB password set during its installation.

galaxy-CoVaCS
-------------

***************
``Description``
***************

Workflow for genotyping and variant annotation of whole genome/exome and target-gene sequencing data (https://www.ncbi.nlm.nih.gov/pubmed/29402227).

*********
``Image``
*********

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-CoVaCS_release_19.05-1.qcow2

******************************
``Tools dependencies tarball``
******************************

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/galaxy-CoVaCS-release_19.05-1.tar.gz

*************
``CMDB json``
*************

Create the file ``cmdb-data/galaxy-CoVaCS.json`` on the CMDB Virtual Machine, with the content:

::

  {
    "type": "image",
    "data": {
        "image_id": "<galaxy-covacs-image-id>",
        "image_name": "centos-7-galaxy-CoVaCS-release_19.05",
        "architecture": "x86_64",
        "type": "linux",
        "distribution": "centos",
        "version": "7",
        "service": "<service-id>"
    }
  }

where ``galaxy-covacs-image-id`` is the image ID on the Cloud platform, while ``service-id`` is the service ID on CMDB.

***********************
``CMDB upload command``
***********************

On CMDB Virtual Machine run the following command:

::

  curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/galaxy-CoVaCS.json

where ``<cmdb_crud_password>`` is the CMDB password set during its installation.

galaxy-GDC_Somatic_Variant
--------------------------

***************
``Description``
***************

Port of the Genomic Data Commons (GDC) pipeline for the identification of somatic variants on whole exome/genome sequencing data (https://gdc.cancer.gov/node/246).

*********
``Image``
*********

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-GDC_Somatic_Variant_release_19.05-1.qcow2

******************************
``Tools dependencies tarball``
******************************

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/galaxy-GDC_Somatic_Variant-release_19.05-1.tar.gz

*************
``CMDB json``
*************

Create the file ``cmdb-data/galaxy-GDC_Somatic_Variant.json`` on the CMDB Virtual Machine, with the content:

::

  {
    "type": "image",
    "data": {
        "image_id": "<galaxy-gdc-image-id>",
        "image_name": "centos-7-galaxy-GDC_Somatic_Variant-release_19.05",
        "architecture": "x86_64",
        "type": "linux",
        "distribution": "centos",
        "version": "7",
        "service": "<service-id>"
    }
  }

where ``galaxy-gdc-image-id`` is the image ID on the Cloud platform, while ``service-id`` is the service ID on CMDB.

***********************
``CMDB upload command``
***********************

On CMDB Virtual Machine run the following command:

::

  curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/galaxy-GDC_Somatic_Variant.json
  {"ok":true,"id":"6e2ed4e065ab0a768d2614fc34005859","rev":"1-edf1bca98184f9a3b08001f96752f214"}

where ``<cmdb_crud_password>`` is the CMDB password set during its installation.

galaxy-epigen
-------------

***************
``Description``
***************

Based on Epigen project (http://www.epigen.it/).

*********
``Image``
*********

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-epigen_release_19.05-1.qcow2

******************************
``Tools dependencies tarball``
******************************

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/galaxy-epigen-release_19.05-1.tar.gz

*************
``CMDB json``
*************

Create the file ``cmdb-data/galaxy-epigen.json`` on the CMDB Virtual Machine, with the content:

::


where ``galaxy-epigen-image-id`` is the image ID on the Cloud platform, while ``service-id`` is the service ID on CMDB.

***********************
``CMDB upload command``
***********************

On CMDB Virtual Machine run the following command:

::


where ``<cmdb_crud_password>`` is the CMDB password set during its installation.

galaxy-rna-workebench
---------------------

***************
``Description``
***************

More than 50 tools for RNA centric analysis (https://www.ncbi.nlm.nih.gov/pubmed/28582575).

*********
``Image``
*********

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-rna-workbench_19.05-1.qcow2

******************************
``Tools dependencies tarball``
******************************

http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/galaxy-rna-workbench-release_19.05-1.tar.gz

*************
``CMDB json``
*************

Create the file ``cmdb-data/galaxy-rna-workbench.json`` on the CMDB Virtual Machine, with the content:

::

  {
    "type": "image",
    "data": {
        "image_id": "<galaxy-rnawb-image-id>",
        "image_name": "centos-7-galaxy-rna-workbench-release_19.05",
        "architecture": "x86_64",
        "type": "linux",
        "distribution": "centos",
        "version": "7",
        "service": "<service-id>"
    }
  }

where ``galaxy-rnawb-image-id`` is the image ID on the Cloud platform, while ``service-id`` is the service ID on CMDB.

***********************
``CMDB upload command``
***********************

On CMDB Virtual Machine run the following command:

::

  curl -X POST http://cmdb:<cmdb_crud_password>@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@cmdb-data/galaxy-rna-workbench.json
  {"ok":true,"id":"6e2ed4e065ab0a768d2614fc34005ad8","rev":"1-bcc95ed3bbb3ca6ef4138d70fb8acab3"}

where ``<cmdb_crud_password>`` is the CMDB password set during its installation.
