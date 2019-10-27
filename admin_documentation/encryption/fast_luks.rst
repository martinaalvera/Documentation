Fast-luks script
================

The ``fast-luks`` script is located in ``/home/galaxy/laniakea_utils/fast-luks``.

It parse common cryptsetup parameters to encrypt the volume. For this reason it checks for cryptsetup and dm-setup packages and it install cryptsetup, if not installed.

Typing ``sudo fast-luks`` the script will load defaults parameters and will LUKS format ``/dev/vdb`` device, otherwise different parameters can be specified.

.. note::

   The script requires superuser rights.

It is mainly made by 5 components:

#. ``fast_luks_encryption.sh``: which is responsible for the encryption.

#. ``fast_luks_volume_setup.sh``: which is in charge of ending volume setup procedure, i.e. format the volume.

#. ``fast_luks.sh``: it is the main script, calling fast_luks_encryption.sh and fast_luks_volume_setup.sh.

#. ``fast_luks_libs.sh``: all the fast_luks function are here.

#. ``defaults.conf``: default configuration file.

After the encryption procedure the script continue running in background using nohup to run the fast_luks_volume_setup.sh script.

Changelog
---------

**Version v3.0.0**
- Add Hashicorp Vault support to store secrets.
- Add non interactive mode allowing to setup passphrases from CLI.
- Add passphrases random generation.

**Version v2.0.0**
- Fix script on background.
- Reworked script with libs, encrpyption, volume setup and main fast luks script.

**Version v1.0.0 (legacy)**
First release.

Options
-------
``-h, --help``: Show help.

``-c, --cipher``: set cipher algorithm [default: aes-xts-plain64].

``-k, --keysize``: set key size [default: 256].

``-a, --hash_algorithm``: set hash algorithm used for key derivation [default: sha256].

``-d, --device``: set device [default: /dev/vdb].

``-e, --cryptdev``: set crypt device [default: cryptdev].

``-m, --mountpoint``: set mount point [default: /export].

``-f, --filesystem``: set filesystem [default: ext4].

``--paranoid-mode``: wipe data after encryption procedure. This take time [default: false].

``--foreground``: run script in foreground [default: false].

**Implement non-interactive mode. Allow to pass password from command line.**

``-n, --non-interactive``: enable non-interactive mode. By default LUKS passphrase has to be interactively inserted. This option allows to pass the passphrase as parameter.

``-p1, --passphrase``: set LUKS passphrase.

``-p2, --verify-passphrase``: verify passphrase.

**Alternatively a random password can be setup.**

``-r, --random-passhrase-generation``: enable random passphrase generation.

**Hashicorp VAULT integration.**

``-v, --vault-url``: Enable passphrase upload on Vault, adding Vault URL.

``-w, --wrapping-token``: specify wrapping token.

``-s --secret-path``: specify secrets path on Vault.

``--key``: specify Vault key name.

**Load defaults.**

``--default``: load default values.

Defaults
--------
``cipher_algorithm``: aes-xts-plain64

``keysize``: 256

``hash_algorithm``: sha256

``device``: /dev/vdb

``cryptdev``: crypt [this is randomly generated]

``mountpoint``: /export

``filesystem``: ext4

``paranoid``: false

``non_interactive``: false

``foreground``: false

Usage
-----
```
# ./fast-luks.sh --defaults
```
