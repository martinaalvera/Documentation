Galaxy instance isolation
=========================
User data are automatically stored to the “/export” directory, where an external (standard block storage) volume is mounted.

All Galaxy job results are stored in this directory through galaxy.ini configuration file. For instance, files directory is located:

::

  # Dataset files are stored in this directory.
  file_path = /export/galaxy/database/files

while the job working directory is located:

::

  # Each job is given a unique empty directory as its current working directory.
  # This option defines in what parent directory those directories will be
  # created.
  job_working_directory = /export/job_work_dir

Here is the list of Galaxy database path directories:

::

  file_path = /export/galaxy/database/files
  job_working_directory = /export/job_work_dir
  new_file_path = /export/galaxy/database/tmp
  template_cache_path = /export/galaxy/database/compiled_templates
  citation_cache_data_dir = /export/galaxy/database/citations/data
  citation_cache_lock_dir = /export/galaxy/database/citations/lock
  whoosh_index_dir = /export/galaxy/database/whoosh_indexes
  object_store_cache_path = /export/galaxy/database/object_store_cache
  cluster_file_directory = /export/galaxy/database/pbs"
  ftp_upload_dir = /export/galaxy/database/ftp

The service offers the possibility to store data exploitng file system encryption or Onedata.

Using file system encryption each Galaxy instance can be deployed as an insulated environment, i.e. data are isolated from any other instance on the same platform and from the cloud service administrators, opening to the adoption of Galaxy based cloud solutions even within clinical environments.
Data privacy is granted through LUKS file system encryption: users will be required to insert a password to encrypt/decrypt data directly on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s). The encryption procedure is described on :doc:`FS_encryption_procedure`.

Alternatively, Users’ data access rights will be controlled through the OneData INDIGO component: .doc.`FS_onedata`

.. toctree::
   :maxdepth: 2

   FS_encryption
   FS_encryption_procedure
   FS_onedata
