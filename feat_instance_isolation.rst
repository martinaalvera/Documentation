Galaxy instance isolation
=========================

Users’ data access rights will be controlled, by default, through the OneData INDIGO component.
Alternatively, each Galaxy instance can be deployed as an insulated environment, i.e. data are isolated from any other instance on the same platform and from the cloud service administrators, opening to the adoption of Galaxy based cloud solutions even within clinical environments.
Data privacy is granted through LUKS file system encryption: users will be required to insert a password to encrypt/decrypt data directly on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s).


.. toctree::
   :maxdepth: 2

   FS_encryption
   FS_encryption_procedure
