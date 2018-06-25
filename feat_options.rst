|project_name| options
======================


job identifier
--------------
``Type``: string

``Description``: Custom job identifier, it will identfy your Galaxy in the job list.

``Mandatory``: No

Virtual hardware configuration
------------------------------

Instance flavor
***************
``Type``: selectable menu (string)

``Description``: Select instance flavor	in terms of virtual CPUs, memory size (RAM) and disk size.

``Mandatory``: Yes

``Sections``: |galaxy_express|, |galaxy_latest|. Available as ``Galaxy server flavor`` on cluster configuration tabs.

Worker node number
******************
``Type``: selectable menu (int)

``Description``: Maximum worker nodes number.

``Mandatory``: Yes

``Sections``: |galaxy_cluster|, |galaxy_elastic_cluster|.

Worker nodes flavor
*******************
``Type``: selectable menu (string)

``Description``: Select worker nodee flavor in terms of virtual CPUs, memory size (RAM) and disk size.

``Mandatory``: Yes

``Sections``: |galaxy_cluster|, |galaxy_elastic_cluster|.


SSH public key
**************
``Type``: string

``Description``: User personale SSH public key. Required to login through SSH in the Galaxy VM

``Mandatory``: Yes

``Sections``: all.

Storage configuration
---------------------

Storage type
************
``Type``: selectable menu (string)

``Description``: Select commont IaaS Block storage (IaaS) or Encrypted Storage (encryption).

``Mandatory``: Yes

``Sections``: all.


Storage size
************
``Type``: selectable menu (string)

``Description``: Select storage size.

``Mandatory``: Yes

``Sections``: all.

Galaxy configuration
--------------------

Galaxy version
**************
``Type``: selectable menu (string)

``Description``: Select Galaxy release version.

``Mandatory``: Yes

``Sections``: all.

Instance description
********************
``Type``: string

``Description``: Customize Galaxy top-left main page badge.

``Mandatory``: No

``Sections``: all.

Galaxy administrator e-mail
***************************
``Type``: string

``Description``: Set galaxy administrator e-mail.

``Mandatory``: Yes

``Sections``: all.

Reference data
**************
``Type``: selectable menu (string)

``Description``: Select reference data CernVM-FS provider.

``Mandatory``: Yes

``Sections``: all.

Tools configuration
-------------------

Galaxy flavors
**************
``Type``: selectable menu (string)

``Description``: Select tools presets to be installed on the server.

``Mandatory``: No

``Sections``: all.
