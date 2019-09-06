Proxy
=====

Setting up PROXY role
---------------------

1. Create and edit proxy.yaml in **group_vars** that contain all the following variables:

   .. highlight:: none

::

 letsencrypt_email: "<email>"
 domain_name: "<control machine HOSTNAME>"

              
.. highlight:: default

Run the role
------------

Run the role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-proxy.yml``

Services end-points
-------------------
.. csv-table:: **Services end-points**
   :header: "Service", "end-point"
   :widths: auto
   :file: ./end_point.csv

