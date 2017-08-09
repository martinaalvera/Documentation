Build Reference Data CernVM-FS server
=====================================

All script needed to deploy a Reference data CernVM-FS Stratum 0 are located here:
https://github.com/indigo-dc/Reference-data-galaxycloud-repository

Create CernVM-FS Repository
---------------------------

The CernVM-FS (cvmfs) relies on OverlayFS or AUFS as default storage driver. Ubuntu 16.04 natively supports OverlayFS, therefore it is used as default, to create and populate the cvmfs server.

Directories
-----------

#. | cvmfs_server_keys/ Public key to mount cvmfs server containing Galaxy Reference Data are located in cvmfs_server_keys/ directory.
#. | heat_template/ Openstack Heat recipes to automatically deploy ad CernVM-FS server.

#. | scripts/ Scripts to populate cvmfs server.
   | fast_mount.sh ---------> Mount external volume
   | refdata_download.py ---> Download reference data
   | refdata_download.sh ---> Exploit refdata_download.py to recursively download all the reference data
   | wget_download.sh ------> use wget to download reference data

#. | lists/ list files (yaml format) to automatically download reference data

Populate a CernVM-FS Repository (with reference data)
----------------------------------------------------

Content Publishing
#. | cvmfs_server transaction <repository name>
#. | Install content into /cvmfs/<repository name>
#. | cvmfs_server publish <repository name>

cvmfs_server publish command will take time to move your contents from /cvmfs/ to /srv/cvmfs/. Enough space should be Once installed on /cvmfs/<repository_name>

Reference data download
-----------------------

fast_mount.sh refdata_download.py refdata_download.sh wget_download.sh

    refdata_download.py
        install python-pycurl package (sudo apt-get install python-pycurl)
        python refata_download.py -i ../lists/hg19-list.yml -o -s <cvmfs_repository_name>

    refdata_download.sh ./refdata_download.sh ../lists/list.txt

    wget_download ../lists/wget_list.txt

Available Reference data

at10-list.yml

at9-list.yml

dm2-list.yml

dm3-list.yml

hg18-list.yml

hg19-list.yml

hg38-list.yml

mm10-list.yml

mm8-list.yml

mm9-list.yml

sacCer1-list.yml

sacCer2-list.yml

sacCer3-list.yml
