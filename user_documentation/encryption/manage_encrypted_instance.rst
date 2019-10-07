Manage an encrypted instance
============================

The service provides the possibility to encrypt the storage volume associated with a Galaxy instance.

.. Warning::

   Only the external volume, where Galaxy data are stored, is encrypted, not the Virtual Machine root disk. The encryption layer should be secure enough to protect data uploaded from users to the Galaxy instance from any unwantend attention. However, users must be aware that the responsibility of correctly handling any sensitive data they upload to Laniakea falls on them and that the administrators of the Laniakea service can not be considered responsible for any data breach that may happen due to neglicence by Galaxy users or the action of external malicious attackers.


Retrieve the encrypted storage passphrase
-----------------------------------------

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


.. figure:: _static/qs_encryption/qs_encryption.png 
   :scale: 70 %
   :align: center
   :alt: Galaxy encryption


Data privacy is granted through LUKS storage encryption: user will be required to insert a password to encrypt/decrypt data directly on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s).

An e-mail is sent to the e-mail address provided the ``Galaxy Configuration`` section.

.. figure:: _static/qs_encryption/qs_encryption_setMail.png 
   :scale: 70 %
   :align: center
   :alt: Galaxy encryption mail configuration section

.. Warning::

   Make sure you have entered a valid mail address!

The e-mail is sent you only when the system is ready to accept your password and contains the instructions to correctly encrypt/decrypt your system. The e-mail subject is ``[ELIXIR-ITALY] Laniakea storage encryption``, sent by ``Laniakea@elixir-italy.org``

.. Warning::

   If you do not receive the e-mail:
  

   #. Check you SPAM mail directory

   #. Chek the spelling of the mail address 


.. figure:: _static/encryption/FS_ecrypt_proc_01.png 
   :scale: 70 %
   :align: center
   :alt: Galaxy encryption mail

Once you get the e-mail  follow the step by step guide to encrypt your volume: :doc:`FS_encryption_procedure`.

User is asked to insert their alphanumeric password 3 times:

#. Set password

#. Confirm password

#. Open LUKS volume.

After the password injection the logout is automatic: the encryption procedure continues in background.

Default encryption algorithm
----------------------------
The default LUKS configuration are:

::

  Cipher: aes-xts-plain64

  Key size: 256 bit

  Hash Algorithm for key derivation: sha256

.. seealso::

   For a detailed description of all Web UI options see section: :doc:`feat_options`.
