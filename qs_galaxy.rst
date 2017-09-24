Get Galaxy
==========

Instantiate Galaxy
------------------

.. Note::

   For a detailed descreption of all Web UI options see section: :doc:`feat_galaxy_custom`.

.. Note::

   To login into the portal see section: :doc:`feat_authentication`.


.. figure:: _static/qs_galaxy/qs_galaxy_FGW.png 
   :scale: 80 %
   :align: center
   :alt: Galaxy express main window

.. figure:: _static/qs_galaxy/qs_galaxy_VirtualHardware.png
   :scale: 30 %
   :align: center
   :alt: Virtual hardware configuration

.. Warning::

   VCPUS and Memory values selected by user have to match Image Flavor presets, otherwise a different flavor, as close as possible to the one selected, will be automatically assigned.
   Please read carefully the section: :doc:`qs_virtual_hdw_presets`.

.. figure:: _static/qs_galaxy/qs_galaxy_SSHkey.png
   :scale: 30 %
   :align: center
   :alt: SSH public key injection

.. figure:: _static/qs_galaxy/qs_galaxy_Storage1.png
   :scale: 30 %
   :align: center
   :alt: Galaxy express Storage section 1

.. figure:: _static/qs_galaxy/qs_galaxy_Storage2.png
   :scale: 30 %
   :align: center
   :alt: Galaxy express Storage section 2

.. figure:: _static/qs_galaxy/qs_galaxy_GalaxyConfig.png
   :scale: 30 %
   :align: center
   :alt: Galaxy express Galxy configuration section

.. figure:: _static/qs_galaxy/qs_galaxy_Tools.png
   :scale: 30 %
   :align: center
   :alt: Galaxy express Tools section

Galaxy login
------------

The galaxy administrator password and the API key are automatically generated during the instatiation procedure and are the same for each instance:

::

  User: your user e-mail

  Password: galaxy_admin_password

  API key: ADMIN_API_KEY

.. Warning::

   Change Galaxy password and the API key as soon as possible!
