Fast-luks script
================

The ``fast-luks`` script is located in ``/usr/local/bin/fast-luks``.

It parse common cryptsetup parameters to encrypt the volume. For this reason it checks for cryptsetup and dm-setup packages and it install cryptsetup, if not installed.

Typing ``sudo fast-luks`` the script will load defaults parameters and will LUKS format ``/dev/vdb`` device, otherwise different parameters can be specified.

NB: Run as root.

===============================  =====================================  ============================================
Argument                         Defaults                               Description
===============================  =====================================  ============================================
``-c``, ``--cipher``             aes-xts-plain64                        Set cipher specification string.
``-k``, ``--keysize``            256                                    Set key size in bits.
``-a``, ``--hash_algorithm``     sha256                                 For luksFormat action specifies hash used\
                                                                        in LUKS key setup scheme and volume\
                                                                        key digest.
``-d``, ``--device``             /dev/vdb                               Set device to be mounted
``-e``, ``--cryptdev``           crypt                                  Sets up a mapping <name> after successful\
                                                                        verification of the supplied key\
                                                                        (via prompting).
``-m``, ``--mountpoint``         /export                                Set mount point
``-f``, ``--filesystem``         ext4                                   Set filesystem
===============================  =====================================  ============================================

::

  $ sudo fast-luks --help
  =========================================================
                        ELIXIR-Italy
                 Filesystem encryption script

  A password with at least 8 alphanumeric string is needed
  There's no way to recover your password.
  Example (automatic random generated passphrase):
                        PcHhaWx4

  You will be required to insert your password 3 times:
    1. Enter passphrase
    2. Verify passphrase
    3. Unlock your volume

  The connection will be  automatically closed.

  =========================================================

  fast-luks: a bash script to automate LUKS file system encryption.
   usage: fast-luks [-h]

   optionals argumets:
   -h, --help           show this help text
   -c, --cipher                 set cipher algorithm [default: aes-xts-plain64]
   -k, --keysize                set key size [default: 256]
   -a, --hash_algorithm         set hash algorithm used for key derivation
   -d, --device                 set device [default: /dev/vdb]
   -e, --cryptdev               set crypt device [default: cryptdev]
   -m, --mountpoint             set mount point [default: /export]
   -f, --filesystem             set filesystem [default: ext4]
   --default                    load default values
