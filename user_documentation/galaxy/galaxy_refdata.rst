Reference Data
==============
Many Galaxy tools rely on the presence of reference data, such as alignment indexes or reference genome sequences, to efficiently work. A complete set of Reference Data, able to work with most common tools for NGS analysis is available for each Galaxy instance deployed.

Available reference data
------------------------
Reference data (e.g. genomic sequences) are available for many species and shared among all the instances, avoiding unnecessary and costly data duplication, exploiting the CernVM-FS filesystem or Onedata.

Until now, Galaxy administrators have been responsible for downloading, building and installing these important reference data. For example, to make the UCSC hg19 build of the human reference genome available to the Burrows-Wheeler Aligner (BWA) short-read mapper (Li and Durbin, 2009), a Galaxy administrator would need to (i) download the reference genome FASTA file, (ii) make it available as a reference genome via the ‘all_fasta’ table (optional), (iii) build BWA alignment indexes via proper command-line calls, (iv) register the location and availability of the indexes within the ‘bwa_indexes’ data table (by adding an additional entry to the tool-data/bwa_index.loc file on disk) and (v) finally, restart the Galaxy server. 

A complete list of the reference data, with download link, is available `here <https://docs.google.com/spreadsheets/d/1sqvpZIJYWuIn5T_P9Iww3y6D1IsHnNmaED3_iE6LAOU/edit?usp=sharing>`_.

::

  Arabidopis thaliana (TAIR9)
  Arabidopis thaliana (TAIR10)
  Drosophila melanogaster (dm3)
  Homo sapiens (hg18)
  Homo sapiens (hg19)
  Homo sapiens (hg38)
  Mus musculus (mm9)
  Mus musculus (mm10)
  Saccharomyces cerevisiae (sacCer3)

.. _fig_updateprocess:

.. figure:: img/refdata_indexes.png
   :scale: 30 %
   :align: center
   :alt: Reference data indexes

   Reference data indexes available for bowite

Homo Sapiens - hg19
*******************

=========================  =================================
Available reference index            Details
=========================  =================================
bowtie
bowtie2
bwa
liftover
rsem                       created with rsem v1.3.0, table and gtf file from ucsc (download date 11 March 2018)
.fa
.2bit
.gtf                       download date: 11 March 2018
=========================  =================================

CernVM-FS reference data
------------------------
The CernVM-File System (conversely cvmfs) provides a scalable, reliable and low- maintenance software distribution service. It was developed to assist High Energy Physics (HEP) collaborations to deploy software on the worldwide- distributed computing infrastructure used to run data processing applications.

CernVM-FS is implemented as a POSIX read-only file system in user space (a FUSE module). The reference data Files and directories are hosted on standard web servers and mounted on ``/refdata`` directory:

::

  $ ls -l /refdata/elixir-italy.galaxy.refdata/
  total 60
  drwxr-xr-x. 5 cvmfs cvmfs 4096 May 21 20:10 at10
  drwxr-xr-x. 5 cvmfs cvmfs 4096 May 21 20:10 at9
  drwxr-xr-x. 3 cvmfs cvmfs 4096 May 21 20:10 dm2
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:11 dm3
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:15 hg18
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 18:36 hg19
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:18 hg38
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:22 mm10
  drwxr-xr-x. 3 cvmfs cvmfs 4096 May 21 20:22 mm8
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:25 mm9
  -rw-r--r--. 1 cvmfs cvmfs   57 May 21 18:31 new_repository
  drwxr-xr-x. 3 cvmfs cvmfs 4096 May 21 20:25 sacCer1
  drwxr-xr-x. 3 cvmfs cvmfs 4096 May 21 20:25 sacCer2
  drwxr-xr-x. 7 cvmfs cvmfs 4096 May 21 20:25 sacCer3
  -rw-r--r--. 1 cvmfs cvmfs    0 May 21 18:31 test-content

Cvmfs client setup
******************
Cvmfs is installed by default on each Galaxy instance (CentOS 7 or Ubuntu 16.04) if this is the reference data configuration provided by your service provider.

The ``elixir-italy.galaxy.refdata.pub`` public key is installed in ``/etc/cvmfs/keys/``. The ``/etc/cvmfs/default.local`` file is also already configured. 

The ``cvmfs_config probe`` command mount the cvmfs volume to ``/cvmfs``, therefore ``mount`` command is used to correctly mount the cvmfs volume to ``/refdata``.

======================  ======================
Description             Command
======================  ======================
check configuration     cvmfs_config chksetup
mount volume            mount -t cvmfs elixir-italy.galaxy.refdata /refdata/elixir-italy.galaxy.refdata
umount volume           cvmfs_config umount elixir-italy.galaxy.refdata
reload repository       cvmfs_config reload elixir-italy.galaxy.refdata
======================  ======================

.. Note::

   If mount fails, try to restart autofs with ``sudo service autofs restart``.

.. Note::

   Cvmfs commands require root privileges

Cvmfs mount output:

::

  $ sudo mount -t cvmfs elixir-italy.galaxy.refdata /refdata/elixir-italy.galaxy.refdata
  CernVM-FS: running with credentials 994:990
  CernVM-FS: loading Fuse module... done

  $ ls /refdata/elixir-italy.galaxy.refdata/
  at10  at9  dm2  dm3  hg18  hg19  hg38  mm10  mm8  mm9  new_repository  sacCer1  sacCer2  sacCer3  test-content

Cvmfs server location
*********************
Current cvmfs server configuration:

=========================  =================================
Reference data cvmfs       Details
=========================  =================================
cvmfs repository name      elixir-italy.galaxy.refdata
cvmfs server url           90.147.102.186
cvmfs key file             `elixir-italy.galaxy.refdata.pub <https://raw.githubusercontent.com/indigo-dc/Reference-data-galaxycloud-repository/master/cvmfs_server_keys/elixir-italy.galaxy.refdata.pub>`_
cvmfs proxy url            DIRECT
=========================  =================================

Troubleshooting
***************
Cvmfs not running, e.g. after reboot:

::

  $ sudo mount -t cvmfs elixir-italy.galaxy.refdata /refdata/elixir-italy.galaxy.refdata
  CernVM-FS: running with credentials 994:990
  CernVM-FS: loading Fuse module... Failed to initialize root file catalog (16 - file catalog failure)

A reload of the config is able to fix the problem: https://wiki.chipp.ch/twiki/bin/view/CmsTier3/IssueCvmfsFailsToMount

::

  $ sudo cvmfs_config reload elixir-italy.galaxy.refdata
  Connecting to CernVM-FS loader... done
  Entering maintenance mode
  Draining out kernel caches (60s)
  Blocking new file system calls
  Waiting for active file system calls
  Saving inode tracker
  Saving chunk tables
  Saving inode generation
  Saving open files counter
  Unloading Fuse module
  Re-Loading Fuse module
  Restoring inode tracker...  done
  Restoring chunk tables...  done
  Restoring inode generation...  done
  Restoring open files counter...  done
  Releasing saved glue buffer
  Releasing chunk tables
  Releasing saved inode generation info
  Releasing open files counter
  Activating Fuse module

Cvmfs server details
********************
Since, cvmfs relies on OverlayFS or AUFS as default storage driver and Ubuntu 16.04 natively supports OverlayFS, it is used as default choice to create and populate the cvmfs server.

A resign script is located in ``/usr/local/bin/Cvmfs-stratum0-resign`` and the corresponding weekly cron job is set to ``/etc/cron.d/cvmfs_server_resign``.

Log file is located in ``/var/log/Cvmfs-stratum0-resign.log``.

Cvmfs references
****************

CernVM-FS: https://cernvm.cern.ch/portal/filesystem

Cvmfs documentation: http://cvmfs.readthedocs.io/en/stable/

Onedata reference data (beta)
-----------------------------
To Be Updated

Reference data local download
-----------------------------
The reference data set can be downloaded on your machine. This option is not explicitly available, by default, on the service web intereface to avoid unuseful replication and costly virtual space consumption.

Nevertheless, it is still possible to download them through ansible and automatically configure galaxy to use them: :doc:`ansible_galaxycloud-refdata`. 
