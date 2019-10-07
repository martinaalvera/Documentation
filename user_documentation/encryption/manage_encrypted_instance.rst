Manage an encrypted instance
============================

Laniakea provides the possibility to encrypt the storage volume associated to the virtual machine on-demand.

A detailed description of Laniakea encryption strategy is reported here: :doc:`/admin_documentation/encryption/encryption`.

.. Warning::

   Only the external volume, where Galaxy data are stored, is encrypted, not the Virtual Machine root disk. The encryption layer should be secure enough to protect data uploaded from users to the Galaxy instance from any unwantend attention. However, users must be aware that the responsibility of correctly handling any sensitive data they upload to Laniakea falls on them and that the administrators of the Laniakea service can not be considered responsible for any data breach that may happen due to neglicence by Galaxy users or the action of external malicious attackers.

Data privacy is granted through LUKS storage encryption: user will be required to insert a password to encrypt/decrypt data directly on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s).

Retrieve the encrypted storage passphrase
-----------------------------------------

Cryptographic keys should never be transmitted in the clear. For this reason during Galaxy deployment user intervention is required.

.. raw:: html

   <p align="center">
   <iframe width="640" height="360"
      src="https://www.youtube.com/embed/G_4aIqkXZTM">
   </iframe> 
   </p>

Restart Galaxy on an encrypted instance
---------------------------------------

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
