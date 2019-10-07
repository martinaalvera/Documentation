Manage encrypted instance
=========================

The service provides the possibility to encrypt the storage volume associated to the virtual machine on-demand.
A detailed description of Laniakea encryption strategy is reported here: :doc:`/admin_documentation/encryption/encryption`.

.. Warning::

   Only the external volume, where Galaxy data are stored, is encrypted, not the Virtual Machine root disk.

Data privacy is granted through LUKS storage encryption: user will be required to insert a password to encrypt/decrypt data directly on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s).

Retrieve encrypted storage passphrase
-------------------------------------

Cryptographic keys should never be transmitted in the clear. For this reason during Galaxy deployment user intervention is required.

.. raw:: html

   <p align="center">
   <iframe width="640" height="360"
      src="https://www.youtube.com/embed/G_4aIqkXZTM">
   </iframe> 
   </p>

Restart Galaxy on encrypted instance
------------------------------------

.. raw:: html

   <p align="center">
   <iframe width="640" height="360"
      src="https://www.youtube.com/embed/g37X8jDSkG4">
   </iframe> 
   </p>

.. note::

   If the automatic procecure does not work, please have a look here: :doc:`/user_documentation/faq/faq`

Default encryption algorithm
----------------------------
The default LUKS configuration are:

::

  Cipher: aes-xts-plain64

  Key size: 256 bit

  Hash Algorithm for key derivation: sha256
