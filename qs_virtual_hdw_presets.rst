Virtual hardware presets
------------------------
Each cloud provider enable a set of Image Flavor, defined in terms of Virctual CPUs (VCPUS), Memory, Disk, etc.
Therefore, it is possible to choose between different Virtual CPUs (VCPUS) and RAM values, corresponding to the available Image Flavors.

.. Warning::

   VCPUS and Memory value selected by user have to match Image Flavor presets, otherwise a different flavor, as close as possible to the one selected, will be automatically assigned.

Currently, the following pre-sets are available:

=========  =======  =======  =============  =============
Name       VCPUS    RAM      Total Disk     Root Disk
=========  =======  =======  =============  =============
small      1        2 GB     20 GB          20 GB
medium 	   2        4 GB     20 GB          20 GB
large      4        8 GB     20 GB          20 GB
xlarge     8        16 GB    20 GB          20 GB
xxlarge    16       32 GB    20 GB          20 GB
=========  =======  =======  =============  =============

New flavors can be assigned to particular projects.
