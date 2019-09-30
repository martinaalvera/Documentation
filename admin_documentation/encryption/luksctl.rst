Luksctl and luksctl APIs
========================

Luksctl
-------

During the encryption procedure ( :doc:`FS_encryption_procedure`), ``fast-luks`` creates a configuration ini file, allowing Galaxy administrator to easily mange LUKS devices, through the ``luksctl`` script (:doc:`script_luksctl`).

By default the file is stored in ``/etc/galaxy/luks-cryptdev.ini``.

The script requires superuser rights.

========  ======================  =========================
Action    Command                 Description
========  ======================  =========================
Open      sudo luksctl open       Open the encrypted device, requiring your passphrase.
Close     sudo luksctl close      Close the encrypted device
Status    sudo luksctl status     Check device status using dm-setup
========  ======================  =========================


Luksctl API
-----------
