File System Encryption
======================

While the adoption of a distributed environment for data analysis makes data difficult to be tracked and identified by a malevolus attacker, full data anonymity and isolation is still not granted.

We have introduced the possibility for the user to isolate data through standard filesystem encryption, based on LUKS (Linux Unified Key Setup), based on cryptsetup and using dm-crypt as the disk encryption backend.

Disk encryption ensures that files are stored on disk in an encrypted form. The files only become available to the operating system and applications in readable when the volume is unlocked by a trusted user. 


form while the system is running and unlocked by a trusted user. An unauthorized person looking at the disk contents directly, will only find garbled random-looking data instead of the actual files. 


Block device encryption methods, on the other hand, operate below the filesystem layer and make sure that everything written to a certain block device (i.e. a whole disk, or a partition, or a file acting as a virtual loop-back device) is encrypted. This means that while the block device is offline, its whole content looks like a large blob of random data, with no way of determining what kind of filesystem and data it contains. Accessing the data happens, again, by mounting the protected container (in this case the block device) to an arbitrary location in a special way. 



adopting the xts-aes encryption algorithm with 256 bit keys.


To automatically setup LUKS volumes on your Galaxy instances a bash script, named ``fast-luks`` (https://github.com/mtangaro/GalaxyCloud/blob/master/LUKS/fast_luks.sh).




A script, named fast-luks and an ansible role (indigo-dc.galaxycloud-os) have been developed to encrypt data and it has been integrated with the Orchestrator. 


data privacy through LUKS filesystem encryption: users will be required to insert a password to encrypt/decrypt data on the virtual instance during its deployment, avoiding any interaction with the cloud administrator(s).




Default configuration
---------------------
# Defaults
cipher_algorithm='aes-xts-plain64'
keysize='256'
hash_algorithm='sha256'
device='/dev/vdb'
cryptdev='crypt'
mountpoint='/export'
filesystem='ext4'



Password choice
---------------




Luksctl
-------

# luks ini file
luks_cryptdev_file='/etc/galaxy/luks-cryptdev.ini'

Fast-luks
---------





References
----------

Disk encryption archlinux wiki page: https://wiki.archlinux.org/index.php/disk_encryption#Block_device_encryption_specific

Dm-crypt archlinux wiki page: https://wiki.archlinux.org/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode

Original LUKS script: https://github.com/JohnTroony/LUKS-OPs/blob/master/luks-ops.sh (Credits to John Troon for the original script))
