Luksctl: LUKS volumes management
================================
Luksctl is a python script allowing to easily Open/Close and Check LUKS encrypted volumes, parsing dmsetup and cryptsetup commands.
The script requires superuser rights.

========  ========
Action    Command
========  ========
Open      sudo luksctl open
Close     sudo luksctl close
Status    sudo luksctl status
========  ========

Dependencies
------------
Since the script is going to parse cryptsetup and dmsetup commands, both are required

::

  cryptsetup

Open LUKS volumes
-----------------
To open LUKS volume, call: ``luksctl open``, which will require your LUKS encrypt password:

::

  $ sudo luksctl open
  Enter passphrase for /dev/disk/by-uuid/9bc8b7c6-dc7e-4aac-9cd7-8b7258facc75:
  Name:              ribqvkjj
  State:             ACTIVE
  Read Ahead:        8192
  Tables present:    LIVE
  Open count:        1
  Event number:      0
  Major, minor:      252, 1
  Number of targets: 1
  UUID: CRYPT-LUKS1-9bc8b7c6dc7e4aac9cd78b7258facc75-ribqvkjj


  Encrypted volume: [ OK ] 

Close LUKS volumes
------------------
To Close LUKS volume, call ``luksctl close``:

::

  $ sudo luksctl close
  Encrypted volume umount: [ OK ]

LUKS volumes status
-------------------
To check if LUKS volume is Open or not call ``luksctl status``

::

  $ sudo luksctl status
  Name:              ribqvkjj
  State:             ACTIVE
  Read Ahead:        8192
  Tables present:    LIVE
  Open count:        1
  Event number:      0
  Major, minor:      252, 1
  Number of targets: 1
  UUID: CRYPT-LUKS1-9bc8b7c6dc7e4aac9cd78b7258facc75-ribqvkjj
  
  
  Encrypted volume: [ OK ]
