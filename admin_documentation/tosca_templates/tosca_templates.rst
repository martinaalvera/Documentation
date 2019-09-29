TOSCA templates
===============

.. figure:: img/tosca_logo.png
   :scale: 100 %
   :align: center
   :alt: TOSCA logo

The :doc:`indigo_orchestrator` is the key software component of the INDIGO PaaS layer, it receives deployment requests from the user interface software layer, and coordinates the deployment process over the IaaS platforms. Then the :doc:`indigo_im` deploysn the customized virtual infrastructure on IaaS Cloud deployment.

The :doc:`indigo_orchestrator` takes the deployment requests written in `TOSCA YAML Simple Profile v1.0 <http://docs.oasis-open.org/tosca/TOSCA-Simple-Profile-YAML/v1.0/TOSCA-Simple-Profile-YAML-v1.0.html>`_. To correctly orchestrate Galaxy deployment the following component are needed:

- Ansible roles: automate software installation and configuration (see section :doc:`dev_ansible_roles`) 
- Custom type: define user configurable parameters, node requirements, call ansible playbooks.
- Artifact: define what to install and how to do it, through ansible role configuration.
- TOSCA template: the orchestrator interprets the TOSCA template and orchestrates the deployment.

.. Note::

   This section is not inteded to be a complete guide to TOSCA types, but aims to describes the solutions adopted to deploy Galaxy.

.. toctree::
   :maxdepth: 2
   :caption: TOSCA documentation

   tosca_customtypes
   tosca_galaxy
   tosca_galaxy_cluster
