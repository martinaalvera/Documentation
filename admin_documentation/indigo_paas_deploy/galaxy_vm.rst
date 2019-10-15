|galaxy_vm| configuration
=========================

|galaxy_vm| exploits custom images with Galaxy, all its companion software and tools inside it. In particular, tools are installed on Galaxy but their dependencies, being bulky and leading to the creation of images that are difficult to manage are compressend in a separated tarball, which is downloaded and extracted at the deployment time.

Image creation
--------------

Image upload
------------

The OS image has to be available in the Tenant.

Tools upload
------------


CMDB configuration
------------------

|galaxy_vm| exploits custom images with Galaxy already inside. Therefore, a naming convention is used, allowing the TOSCA template to call the right image: ``centos-7-<galaxy_flavour>-<galaxy_version>``, where ``<galaxy_flavour≤`` is the selected flavour and ``<galaxy_version`` ins the selected Galaxy version.

Therefore, the image name uploaded on CMDB must follow this convention. For example, if the ``galaxy_flavour = galaxy-CoVaCS`` and the ``galaxy_version = release_19.05`` the resultant image name will be ``centos-7-galaxy-CoVaCS-release_19.05``.



TOSCA template configuration
----------------------------

The TOSCA template, using the user input, rebuild the image name and retrieve the right one:

::

  galaxy_server:
  ...
      # Guest Operating System properties
      os:
        properties:
          image: { concat: ['centos-7-', get_input: flavor,'-', get_input: version ] } # centos-7-galaxy-CoVaCS-release_19.05
  ...

The image prefix ``centos-7`` is arbitrary and can be modified, but it must be the same on the CMDB image name and the TOSCA template.

Finally


::

    remote_tool_deps_dir_url:
      type: string
      description: tools tar gz location
      default: 'http://cloud.recas.ba.infn.it:8080/v1/AUTH_3b4918e0a982493e8c3ebcc43586a2a8/Laniakea-generic-cloud-images'



******************
``galaxy-minimal``
******************


:Image:
	http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-minimal_release_19.05-1.qcow2

:CMDB json:
	::

	  {
	    "type": "image",
	    "data": {
	        "image_id": "a3c9f9b4-7266-4982-b444-f658da84f3d6",
	        "image_name": "centos-7-galaxy-minimal-release_19.05",
	        "architecture": "x86_64",
	        "type": "linux",
	        "distribution": "centos",
	        "version": "7",
	        "service": "service-RECAS-BARI-openstack"
	    }
	  }

******************
``galaxy-CoVaCS``
******************

:Image:
	http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/CentOS-7-x86_64-GenericCloud_galaxy-CoVaCS_release_19.05-1.qcow2

:Tools tar.gz:
	http://cloud.recas.ba.infn.it/horizon/api/swift/containers/Laniakea-generic-cloud-images/object/galaxy-CoVaCS-release_19.05-1.tar.gz

:CMDB json:
	::

	  {
	    "type": "image",
	    "data": {
	        "image_id": "0a4bca8d-8e7c-43bf-aee1-21cb9057c1d9",
	        "image_name": "centos-7-galaxy-CoVaCS-release_19.05",
	        "architecture": "x86_64",
	        "type": "linux",
	        "distribution": "centos",
	        "version": "7",
	        "service": "service-RECAS-BARI-openstack"
	    }
	  }


******************************
``galaxy-GDC_Somatic_Variant``
******************************


*****************
``galaxy-epigen``
*****************


*************************
``galaxy-rna-workebench``
*************************
