Proxy server
============
A proxy server is used to expose IM, CMDB, CPR and the PaaS Orchestrator.

VM configuration
----------------

The master VM can used to run the proxy server. The VM should meet the following minimum requirements:

::

  OS: Ubuntu 16.04 VM
  vCPUs: 2 vCPUs
  RAM:4 GB of RAM
  Network: a private and a public IP address and the SSH public key configuration to allow Ansible to connect to the remote VM.

.. warning::

   All the command will be run on the ``master`` VM.

Installation
------------

Create the file ``indigopaas-deploy/ansible/inventory/group_vars/proxy.yaml`` with the following configured values:

::

 letsencrypt_email: "<valid_email_address>"
 domain_name: "<proxy_vm_dns_name>"

.. warning::

   Please provide a valid e-mail address, which is mandatory for Let's Encrypt certificate creation.              

Run the role using ``ansible-playbook``

::

  # cd indigopaas-deploy/ansible

  # ansible-playbook -i inventory/inventory playbooks/deploy-proxy.yml

Video tutorial
--------------

.. raw:: html

   <script id="asciicast-RHPlUmQGfGT1cPx4hGDOMWqAv" src="https://asciinema.org/a/RHPlUmQGfGT1cPx4hGDOMWqAv.js" async></script>
