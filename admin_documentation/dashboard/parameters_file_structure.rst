File structure
==============

The YAML parameter file has two sections: ``tabs`` and ``ìnputs``.

--------
``tabs``
--------

:Description:
	This section is optional, if set creates the listed tabs instead of the ``Input values`` one. It is possible to display each input in the desired tab, using the option ``tab`` in the input section. If not specified, all inputs will be displayed by default in the ``Ìnput values`` tab, as default behaviour.

:Example:
	::

	  # Set here the list of the tabs to be displayed
	  tabs: [ "tab_1", "tab_2"]
	  ...

----------
``inputs``
----------

:Description:
	The list of the inputs is mandatory. Each input must have the same name of the corresponding TOSCA template input value, to be correctly associated.

:Example:
	::
	
	  # Set here the list of the tabs to be displayed
	  tabs: [ "tab_1", "tab_2"]
	  
	  # Set here a new set of inputs to be displayed
	  inputs:
	  
	    first_input:
	      display_name: "<name to be displayed>"
	      tag_type: "<specific tag type for this input>"
	      description: "<description to desplayed>"
	      tab: "tab_1"
	
	    another_input:
	      display_name: "<name to be displayed>"
	      tag_type: "<specific tag type for this input>"
	      description: "<description to desplayed>"
	      tab: "tab_2"
	
	    ...

--------------------
``Supported inputs``
--------------------

``instance_flavor_fe``: if an input with the same name is used in the TOSCA template, this variable does not trigger any special action. If not, the correspondig menu accepts couples of **number of CPUs** and **RAM size** in the form of python dictionary: ``{'<tosca_template_cpu_num>':'2', '<tosca_template_mem_size>':'4 GB'}``. ``instance_flavor_fe`` is commonly used for front-end inputs.

``tosca_template_cpu_num`` and ``tosca_template_mem_size`` are the corresponding inputs in the TOSCA template. For example, if in the TOSCA template you have:

::

  ...

  topology_template:
    inputs:
  
      fe_cpus:
        type: integer
        description: Numer of CPUs for the front-end node
        default: 1
        required: yes
  
      fe_mem:
        type: scalar-unit.size
        description: Amount of Memory for the front-end node
        default: 1 GB
        required: yes
  
    ...

The corresponding entry in the parameter file will be:

::

  instance_flavor_fe:
    display_name: "Front End instance flavour"
    tag_type: "select"
    description: "CPUs, memory size (RAM), root disk size"
    constraints:
      - { value: "{'fe_cpus':'2', 'fe_mem':'4 GB'}", label: "Medium (2 cpu, 4 GB RAM, 20 GB dsk)" }
      - { value: "{'fe_cpus':'4', 'fe_mem':'8 GB'}", label: "Large (4 cpu, 8 GB RAM, 20 GB dsk)" }
      - { value: "{'fe_cpus':'8', 'fe_mem':'16 GB'}", label: "xLarge (8 cpu, 16 GB RAM, 20 GB dsk)" }


``instance_flavor_wn``: if an input with the same name is used in the TOSCA template, this variable does not trigger any special action. If not, the correspondig menu accepts couples of **number of CPUs** and **RAM size** in the form of python dictionary: ``{'<tosca_template_cpu_num>':'2', '<tosca_template_mem_size>':'4 GB'}``. ``instance_flavor_wn`` is commonly used for front-end inputs.

``tosca_template_cpu_num`` and ``tosca_template_mem_size`` are the corresponding inputs in the TOSCA template. For example, if in the TOSCA template you have:

::

  ...
  topology_template:
    inputs:
      wn_cpus:
        type: integer
        description: Numer of CPUs for the WNs
        default: 1
        required: yes
  
      wn_mem:
        type: scalar-unit.size
        description: Amount of Memory for the WNs
        default: 1 GB
        required: yes
  ...

The corresponding entry in the parameter file will be:

::

  instance_flavor_wn:
    display_name: "Worker Node nstance flavour"
    tag_type: "select"
    description: "CPUs, memory size (RAM), root disk size"
    constraints:
      - { value: "{'wn_cpus':'2', 'wn_mem':'4 GB'}", label: "Medium (2 cpu, 4 GB RAM, 20 GB dsk)" }
      - { value: "{'wn_cpus':'4', 'wn_mem':'8 GB'}", label: "Large (4 cpu, 8 GB RAM, 20 GB dsk)" }
      - { value: "{'wn_cpus':'8', 'wn_mem':'16 GB'}", label: "xLarge (8 cpu, 16 GB RAM, 20 GB dsk)" }


.. note::

   For the full list of supported tag types, see section: :doc:`parameters_tags`.
