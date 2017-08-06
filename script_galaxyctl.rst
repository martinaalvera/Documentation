Galaxyctl: Galaxy management
============================
Galaxyctl is a python script collection used for Galaxy management. In particular it exploits ``galaxyctl_libs`` to properly check uWSGI Stats sto correctly retrieve Galaxy and uWSGI workers status.
Moreover the script allow to manage, using the same command, luks volume and onedata spaces, parsing ``luksctl`` and ``onedatctl`` commands.

Since the script parse ``supervisorctl`` or ``systemd`` commands, it needs to be run as superuser.

===========  =========  ====================
Moudule      Action     Description
===========  =========  ====================
galaxy       status     Show galaxy status
|            stop       Stop Galaxy.
|            start      Start Galaxy. ``--force`` force galaxy to start by restarting it. ``--retry`` option allow to specify number of tentative retart (default 5). ``--timeout`` allow to customize uWSGI stats server wait time. These options are used during galaxy instantiation and you should not use them on production.
|            restart      Restart Galaxy. ``--force`` force galaxy to start by restarting it. ``--retry`` option allow to specify number of tentative retart (default 5). ``--timeout`` allow to customize uWSGI stats server wait time. These options are used during galaxy instantiation and you should not use them on production.
|            startup    This method is used only to run galaxy for the first time.
luks         status     Show LUKS volume status
|            open       LUKSOpen volume
|            close      LUKSClose volume
onedata      status     Show onedata space status. ``--userdata`` allow to check user data space if mounte through oneclient. ``--refdata`` allow to check reference data onedata space if mounted through oneclient.
|            mount      Mount onedata space using oneclient. Use ``--userdata`` or ``--refdata`` to mount user data and reference data volumes.
|            umount     Umount onedata space using furermount.
===========  =========  ====================

Command layout
--------------


Galaxy start/stop/restart/status
-----------
To stop galaxy:
::
  sudo galaxyctl stop galaxy

The script check the uWSGI Stats server to retrieve workers PID and their status. If, after uWSGI stop, workers are still up and running, they are killed, allowing Galaxy to correctly start next time.

To start Galaxy:
::
  sudo galaxyctl start galaxy

Once Galaxy started, galaxyctl waits and check the uWSGI Stats server. Since it is the last software loaded, this ensure that Galaxy has correctly started.
The script also check that at least 1 uWSGI worker has correctly started and it is accepting requests.

If no workers are available you have to restart Galaxy.
Galaxyctl is able to automatically restart galaxy if the option ``--force`` is specified, restarting it until the workers are correctly loaded
The number of retries is set, by default, to 5. It can be customized using ``--retry`` option, e.g. ``--retry 10``.
These options were not designed for production, but are used only during VMs instantiation phase to ensure Galaxy can correctly start.

To restart Galaxy:
::
  sudo galaxyctl restart galaxy

The options ``--force``, ``--timeout`` and ``--retry`` are available for restart command too.

To display Galaxy status:
::
  sudo galaxyctl status galaxy


Galaxy first start
------------------


The check-galaxy command in Referece data ansible role

LUKS module
-----------
By parsing luksctl script and using galaxyctl_libs, galaxyctl is able to manage LUKS volumes
To unlock you LUKS volume:
::
  sudo galaxyctl open luks

Then you will be asket to insert your LUKS passphrase. For instance:

::

   (.venv) [galaxy@galaxy-indigo-test ~]$ sudo ./galaxyctl open luks
   Enter passphrase for /dev/disk/by-uuid/42aaf979-6351-44e9-97ee-19e7f8c5e9f6: 

To close your LUKS volume: 
::
  sudo galaxyctl close luks

Finally to chke LUKS volume status:
::
  sudo galaxyctl status luks

Onedata module
--------------
By parsing onedatactl script and using galaxyctl_libs, galaxyctl is able to manage onedata user data and reference data spaces.
We are going to refere in this brief how-to to userdata, but the same commands works to load reference data spaces, simbly adding ``--userdata`` or ``--refdata`` to galaxyctl commands.
The options ``--userdata`` and ``--refdata`` are mutually exclusive.

To mount onedata space volume:
::
  sudo galaxyctl mount onedata --userdata

To umount onedata space volume:
::
  sudo galaxyctl umount onedata --userdata

Finally to check onedata space status:
::
  sudo galaxyctl status onedata --userdata

Configuration files
-------------------

# Init system
# Supported: supervisord, init
# supervisord ---> Current default, it is mandatory for docker container, since there's no systemd.
# init ----------> CentOS 7 and Ubuntu 16.04 use systemd, Ubuntu 14.04 is using upstart.

init_system = 'supervisord'

Through ``galaxyctl_libs.DetectGalaxyCommands`` method the script is compatible with both CentOS 7 and Ubuntu (14.04 and 16.04).

If Supervisord is used to manage Galaxy (which is our default choice), configuration files have to be specified using the variable ``supervisord_config_file``
CentOS configuration:
::
  supervisord_conf_file = '/etc/supervisord.conf'
Ubuntu configuration:
::
  supervisord_conf_file = '/etc/supervisor/supervisord.conf'



galaxy_config_file = '/home/galaxy/galaxy/config/galaxy.ini'
luks_config_file = '/etc/galaxy/luks-cryptdev.ini'
luksctl_path = '/home/galaxy'
onedatactl_config_file = '/etc/galaxy/onedatactl.ini'
onedatactl_path = '/home/galaxy'

Logging
-------
Galaxyctl log file is located in ``/var/log/galaxy/galaxyctl.log``.
