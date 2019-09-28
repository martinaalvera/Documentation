Custom types
============

GalaxyPortal
------------
Galaxy portal installation and configuration is entrusted to the GalaxyPortal custom type:

#. Galaxy instance input parameters:

   ::

    properties:
      admin_email:
        type: string
        description: email of the admin user
        default: admin@admin.com
        required: false
      admin_api_key:
        type: string
        description: key to access the API with admin role
        default: not_very_secret_api_key
        required: false
      user:
        type: string
        description: username to launch the galaxy daemon
        default: galaxy
        required: false
      install_path:
        type: string
        description: path to install the galaxy tool
        default: /home/galaxy/galaxy
        required: false
      export_dir:
        type: string
        description: path to store galaxy data
        default: /export
        required: false
      version:
        type: string
        description: galaxy version to install
        default: master
        required: false
      instance_description:
        type: string
        description: galaxy instance description
        default: "INDIGO Galaxy test"
      instance_key_pub:
        type: string
        description: galaxy instance ssh public key
        default: your_ssh_public_key

   .. Note::

      The ``export_dir`` property is able to set Galaxy storage location. On single VMs it is set to ``/export``, while on Cluster it has to be set to ``/home/export``, allowing for data sharing.

#. Specify LRMS, e.g.  local, torque, slurm, sge, condor, mesos:

   ::

    requirements:
      - lrms:
          capability: tosca.capabilities.indigo.LRMS
          node: tosca.nodes.indigo.LRMS.FrontEnd
          relationship: tosca.relationships.HostedOn

#. Ansible role installation through ansible-galaxy:

   ::

    artifacts:
      galaxy_role:
        file: indigo-dc.galaxycloud
        type: tosca.artifacts.AnsibleGalaxy.role


#. Ansible role call with input parameters:

   ::

    implementation: https://raw.githubusercontent.com/indigo-dc/tosca-types/master/artifacts/galaxy/galaxy_install.yml
          inputs:
            galaxy_install_path: { get_property: [ SELF, install_path ] }
            galaxy_user: { get_property: [ SELF, user ] }
            galaxy_admin: { get_property: [ SELF, admin_email ] }
            galaxy_admin_api_key: { get_property: [ SELF, admin_api_key ] }
            galaxy_lrms: { get_property: [ SELF, lrms, type ] }
            galaxy_version: { get_property: [ SELF, version ] }
            galaxy_instance_description: { get_property: [ SELF, instance_description ] }
            galaxy_instance_key_pub:  { get_property: [ SELF, instance_key_pub ] }
            export_dir: { get_property: [ SELF, export_dir ] }

#. The artifact is located on github `tosca-types/artifacts/galaxy/galaxy_install.yml <https://github.com/indigo-dc/tosca-types/blob/mtangaro-galaxy-tools/artifacts/galaxy/galaxy_install.yml>`_

   ::

    ---
    - hosts: localhost
      connection: local
      roles:
        - role: indigo-dc.galaxycloud
          GALAXY_VERSION: "{{ galaxy_version }}"
          GALAXY_ADMIN_EMAIL: "{{ galaxy_admin }}"
          GALAXY_ADMIN_API_KEY: "{{ galaxy_admin_api_key }}"


GalaxyPortalAndStorage
----------------------
GalaxyPortalAndStorage custom type inherits its properties from GalaxyPortal and extends its functionalities with onedata support and file system encryption:

#. Storage options properties:

   ::

      os_storage:
        type: string
        description: Storage type (Iaas Block Storage (default), Onedaata, Filesystem encryption)
        default: "IaaS"
        required: true
      token:
        type: string
        description: Access token for onedata space
        default: "not_a_token"
        required: false
      provider:
        type: string
        description: default OneProvider
        default: "not_a_provider_url"
        required: false
      space:
        type: string
        description: Onedata space
        default: "galaxy"
        required: false

#. Ansible roles: oneclient role is needed to install oneclient, while indigo-dc.galaxycloud-os is entrusted of file system encryption:

   ::

      oneclient_role:
        file: indigo-dc.oneclient
        type: tosca.artifacts.AnsibleGalaxy.role
      galaxy_os_role:
        file: indigo-dc.galaxycloud-os
        type: tosca.artifacts.AnsibleGalaxy.role
      galaxy_role:
        file: indigo-dc.galaxycloud
        type: tosca.artifacts.AnsibleGalaxy.role

#. Ansible role call with input parameters:

   ::

          implementation: https://raw.githubusercontent.com/indigo-dc/tosca-types/master/artifacts/galaxy/galaxy_os_install.yml
          inputs:
            os_storage: { get_property: [ SELF, os_storage ] }
            userdata_token: { get_property: [ SELF, token ] }
            userdata_oneprovider: { get_property: [ SELF, provider ] }
            userdata_space: { get_property: [ SELF, space ] }
            galaxy_install_path: { get_property: [ SELF, install_path ] }
            galaxy_user: { get_property: [ SELF, user ] }
            galaxy_admin: { get_property: [ SELF, admin_email ] }
            galaxy_admin_api_key: { get_property: [ SELF, admin_api_key ] }
            galaxy_lrms: { get_property: [ SELF, lrms, type ] }
            galaxy_version: { get_property: [ SELF, version ] }
            galaxy_instance_description: { get_property: [ SELF, instance_description ] }
            galaxy_instance_key_pub:  { get_property: [ SELF, instance_key_pub ] }
            export_dir: { get_property: [ SELF, export_dir ] }

#. The artifact includes indigo-dc.galaxycloud-os and indigo-dc.galaxycloud call. 

   ::

     ---
     - hosts: localhost
       connection: local
       roles:
         - role: indigo-dc.galaxycloud-os
           GALAXY_ADMIN_EMAIL: "{{ galaxy_admin }}"

         - role: indigo-dc.galaxycloud
           GALAXY_VERSION: "{{ galaxy_version }}"
           GALAXY_ADMIN_EMAIL: "{{ galaxy_admin }}"
           GALAXY_ADMIN_API_KEY: "{{ galaxy_admin_api_key }}"
           enable_storage_advanced_options: true # true only with indigo-dc.galaxycloud-os


   .. Note::

      The option ``enable_storage_advanced_options`` has to be set to ``true``, leaving storage configuration to indigo-dc.galaxycloud-os.

GalaxyShedTool
--------------

#. Ansible Galaxy tools properties:

   ::

    properties:
      flavor:
        type: string
        description: name of the Galaxy flavor
        required: true
        default: galaxy-no-tools
      admin_api_key:
        type: string
        description: key to access the API with admin role
        default: not_very_secret_api_key
        required: false

#. Galaxy is required:

   ::
    requirements:
      - host:
          capability: tosca.capabilities.Container
          node: tosca.nodes.indigo.GalaxyPortal
          relationship: tosca.relationships.HostedOn

#. Indigo-dc.galaxy-tools role installation:

   ::

    artifacts:
      galaxy_role:
        file: indigo-dc.galaxy-tools,master
        type: tosca.artifacts.AnsibleGalaxy.role

#. Ansible role call. Instance IP address is needed to install tools:

   ::

          implementation: https://raw.githubusercontent.com/indigo-dc/tosca-types/master/artifacts/galaxy/galaxy_tools_configure.yml
          inputs:
            galaxy_flavor: { get_property: [ SELF, flavor ] }
            galaxy_admin_api_key: { get_property: [ HOST, admin_api_key ] }
            instance_public_ip: { get_attribute: [ HOST, public_address, 0 ] }


#. The artifact checks if Galaxy is on-line before installing tools and downloads yaml tool list according to ``galaxy_flavor`` variable value.

   ::

     ---
     - hosts: localhost
       connection: local
       gather_facts: False
       pre_tasks:
         - name: Wait Galaxy is up
           uri: url="http://{{ instance_public_ip }}/galaxy/"
           register: result
           until: result.status == 200
           retries: 30
           delay: 10
           when: galaxy_flavor != 'galaxy-no-tools'
         - name: Get tool-list
           get_url: url="https://raw.githubusercontent.com/indigo-dc/Galaxy-flavors-recipes/master/galaxy-flavors/{{ galaxy_flavor }}-tool-list.yml" dest="/tmp/"
           when: galaxy_flavor != 'galaxy-no-tools'
       vars:
         galaxy_tools_tool_list_files: [ "/tmp/{{ galaxy_flavor }}-tool-list.yml" ]
         galaxy_tools_galaxy_instance_url: "http://{{ instance_public_ip }}/galaxy/"
         galaxy_tools_api_key: "{{ galaxy_admin_api_key }}"
       roles:
         - { role: indigo-dc.galaxy-tools, when: galaxy_flavor != 'galaxy-no-tools' }

   .. Note::

      ``gather_facts: False`` is needed to properly set ansible variables. 

GalaxyReferenceData
-------------------
The ReferenceData custom type supports CernVM-FS, Onedata reference data volumes and reference data downloads.

#. ReferenceData input parameters:

   ::

    properties:
      reference_data:
        type: boolean
        description: Install Reference data
        default: true
        required: true
      flavor:
        type: string
        description: name of the Galaxy flavor
        required: true
        default: galaxy-no-tools
      refdata_repository_name:
        type: string
        description: Onedata space name, CernVM-FS repository name or subdirectory downaload name
        default: 'elixir-italy.galaxy.refdata'
        required: false
      refdata_provider_type:
        type: string
        description: Select Reference data provider type (Onedata, CernVM-FS or download)
        default: 'onedata'
        required: false
      refdata_provider:
        type: string
        description: Oneprovider for reference data
        default: 'not_a_provider'
        required: false
      refdata_token:
        type: string
        description: Access token for reference data
        default: 'not_a_token'
        required: false
      refdata_cvmfs_server_url:
        type: string
        description: CernVM-FS server, replica or stratum-zero
        default: 'server_url'
        required: false
      refdata_cvmfs_repository_name:
        type: string
        description: Reference data CernVM-FS repository name
        default: 'not_a_cvmfs_repository_name'
        requred: false
      refdata_cvmfs_key_file:
        type: string
        description: CernVM-FS public key
        default: 'not_a_key'
        required: false
      refdata_cvmfs_proxy_url:
        type: string
        description: CernVM-FS proxy url
        default: 'DIRECT'
        required: false
      refdata_cvmfs_proxy_port:
        type: integer 
        description: CernVM-FS proxy port
        default: 80
        required: false
      refdata_dir:
        type: string
        description: path to store galaxy reference data
        default: /refdata
        required: false

#. Galaxy is required to install and configure reference data:

   ::

    requirements:
      - host:
          capability: tosca.capabilities.Container
          node: tosca.nodes.indigo.GalaxyPortal
          relationship: tosca.relationships.HostedOn

#. Cvmfs role is used to install cvmfs client if cvmfs is selected to provide reference data. Oneclient role is used to provide onedata support.

    artifacts:
      oneclient_role:
        file: indigo-dc.oneclient
        type: tosca.artifacts.AnsibleGalaxy.role
      cvmfs_role:
        file: indigo-dc.cvmfs-client
        type: tosca.artifacts.AnsibleGalaxy.role
      galaxy_role:
        file: indigo-dc.galaxycloud-refdata
        type: tosca.artifacts.AnsibleGalaxy.role

#. Ansible role call with paramteres:

   ::

          implementation: https://raw.githubusercontent.com/indigo-dc/tosca-types/master/artifacts/galaxy/galaxy_redfata_configure.yml
          inputs:
            get_refdata: { get_property: [ SELF, reference_data ] }
            galaxy_flavor: { get_property: [ SELF, flavor ] }
            refdata_repository_name: { get_property: [ SELF, refdata_repository_name ] }
            refdata_provider_type: { get_property: [ SELF, refdata_provider_type ] }
            refdata_provider: { get_property: [ SELF, refdata_provider ] }
            refdata_token: { get_property: [ SELF, refdata_token ] }
            refdata_cvmfs_server_url: { get_property: [ SELF, refdata_cvmfs_server_url ] }
            refdata_cvmfs_repository_name: { get_property: [ SELF, refdata_cvmfs_repository_name ] }
            refdata_cvmfs_key_file: { get_property: [ SELF, refdata_cvmfs_key_file ] }
            refdata_cvmfs_proxy_url: { get_property: [ SELF, refdata_cvmfs_proxy_url ] }
            refdata_cvmfs_proxy_port: { get_property: [ SELF, refdata_cvmfs_proxy_port ] }
            refdata_dir: { get_property: [ SELF, refdata_dir ] }

#. Cvmfs public key is downloaded to mount cvmfs volume: 

   ::

     ---
     - hosts: localhost
       connection: local
       pre_tasks:
         - name: Get refdata-list
           get_url:
           url: 'https://raw.githubusercontent.com/indigo-dc/Reference-data-galaxycloud-repository/master/cvmfs_server_keys/{{ refdata_cvmfs_key_file }}'
           dest: '/tmp'
       roles:
         - role: indigo-dc.galaxycloud-refdata
