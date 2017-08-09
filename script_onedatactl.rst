Onedatactl: Onedata spaces management
=====================================
Onedatactl is a python script to mount Onedata spaces, for user data and reference data.
This script parse oneclient options using a configuration file (onedatactl.ini) to retrieve the required onedata space information (e.g. oneprovider, token and mountpoint).

Options
-------
Parsing all oneclient option is out of the purpose of this script.
Therfore the script provides only few options to allow user to easily mount their data hosted on onedata

=======================  =======================
Option                   Description
=======================  =======================
mount                    Mount user data or reference data space.
umount                   Umount user data or reference data space.
``-t`` ``--token``       Set access token.
``-H`` ``--provider``    Set onedata provider.
``-m`` ``--mountpoint``  Set mountpoint.
``-c`` ``config_file``   Load configuration file.
``--insecure``           Allow insecure mount.
``--nonempty``           Mount space on non empty space.
``--version``            Show galaxyctl_libs version.
=======================  =======================

The onedatactl.ini file
-------------------
Onedatactl.ini file is located in ``/etc/galaxy/onedatactl.ini``.
The ini file has two secitons: ``[userdata]`` for user data management and ``refdata`` for reference data mangement.

mountpoint
**********
By enabling this option onedata space will be used to store user data and it will be mounted on the specified directory, e.g. ``/export``
This argument is required.

::

  mountpoint = /export

provider
********
Insert Onedata provider for user data, e.g. oneprovider2.cloud.ba.infn.it
This argument is required.

::
 
  provider = oneprovider2.cloud.ba.infn.it

token
*****
Insert Onedata token for user data.
This argument is required.

::

  token = MDAxNWxvY2F00aW9uIG9uZXpvbmUKMDAzYmlkZW500aWZpZXIgeExqMi00xdFN3YVp1VWIxM1dFSzRoNEdkb2x3cXVwTnpSaGZONXJSN2tZUQowMDFhY2lkIHRpbWUgPCAxNTI1MzM00NzgyCjAwMmZzaWduYXR1cmUgIOzeMtypO75nZvPJdAocInNbgH9zvJi6ifgXDrFVCr00K

insecure
********
Allow insecure connection. This is an optional argument.

::

  insecure = False

nonempty
********
Allow to mount space on non empty directory. This is an optional argument

::

  nonempty = False

Onedatactl options
------------------
The script allow to mount two different volumes.

mount
*****
For user data, call:
::

  sudo onedatactl mount userdata

For reference data, call:
::

  sudo onedatactl mount refdata

umount
******
For user data, call:
::

  sudo onedatactl umount userdata

For reference data, call:
::

  sudo onedatactl umount refdata

status
******
For user data, call:
::

  sudo onedatactl status userdata

For reference data, call:
::

  sudo onedatactl status refdata


Oneclient
---------
Onedatactl parse oneclient command using the information stored in ``/etc/galaxy/onedatactl.ini`` file.
Therefore oneclient can be used to perform the same actions.

The basic command line syntax to mount spaces using a specific Oneprovider is:

::

  oneclient -H <PROVIDER_HOSTNAME> -t <ACCESS_TOKEN> <MOUNT_POINT>

In order to unmount your spaces, type:

::

  oneclient -u MOUNT_POINT

The complete Oneclient documentation is located here: https://onedata.org/docs/doc/using_onedata/oneclient.html

Troubleshooting
---------------

If you are connecting to a provider service which does not have a globally trusted certificate, you will have to use ``--insecure`` option.
