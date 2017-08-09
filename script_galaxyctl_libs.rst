Galaxyctl libraries
===================
Galaxyctl is a paython script collenction for Galaxy management (first start, stop/start/restart/status). Moreover it is possible to manage, through specific script, LUKS volumes and Onedata spaces.

Current version: ``0.0.1``

================  ================
Script            Description
================  ================
galaxyctl_libs    Python libraries for uWSGI socket and stats server management, LUKS volume and Onedata space management.
galaxyctl         Galaxy management script. It integrates Luksctl and Onedatactl commands.
luksctl           LUKS volume script management
onedatactl        Onedata spaces for user data and reference data management.
================  ================

Galaxyctl_libs is composed by several modules.

Dependencies
------------

Galaxyctl_libs depends on ``uWSGI`` for Galaxy management (i.e. currently no run.sh support). Morover ``lsof`` is needed to check listening ports.

::

  uwsgi
  
  lsof


DetectGalaxyCommands
--------------------
Parse galaxy Stop/Start/Restart/Status commands. Currently it supports supervisord or systemd/upstart

UwsgiSocket
-----------
Get uWSGI socket from galaxy.ini config file (e.g. 127.0.0.1:4001) and using ``lsof`` return uWSGI master PID.

::

  master_pid, stderr, status = UwsgiSocket(fname='/home/galaxy/galaxy/config/galaxy.ini').get_uwsgi_master_pid()

UwsgiStatsServer
----------------
Read uWSGI stats server json.
The stats server is the last software which uWSGI run during galaxy start procedure. When the stats server is ready, galaxy is ready to accept requests.
Stats server address and port can be specified, but the class is able to read galaxy.ini file to recover stats informations.
Reading Stats json the class is able to detect if uWSGI workers accept requests or not.

=========  ====================
Inputs     Description
=========  ====================
server     uWSGI stats server address, e.g. 127.0.0.1
port       uUWSG stats server port, e.g. 9191
timeout    Wait time, in seconds, for the Stats server start. If galaxy is starting, ``300`` seconds as timeout is ok, while if galaxy is already running ``5`` seconds are enough.
fname      Galaxy config file, e.g. /home/galaxy/galaxy/config/galaxy.ini
=========  ====================

GetUwsgiStatsServer
*******************
To connect to running uWSGI stats server call:

::

   stats = UwsgiStatsServer(timeout=300, fname='/home/galaxy/galaxy/config/galaxy.ini)
   socket = stats.GetUwsgiStatsServer()

GetUwsgiStatsServer
*******************
To check if at least one uWSGI workers accept requests, call:

::

   stats = UwsgiStatsServer(timeout=300, fname='/home/galaxy/galaxy/config/galaxy.ini)
   status = stats.GetUwsgiStatsServer('/home/galaxy/galaxy/config/galaxy,ini')

GetBusyList
***********
To get the list of busy uWSGI workers:

::

  stats = UwsgiStatsServer(timeout=5, fname='/home/galaxy/galaxy/config/galaxy.ini)
  busy_list = stats.GetBusyList()

LUKSCtl
-------
Read LUKS ini file, usually stored on ``/etc/galaxy/luks-cryptdev.ini``, for LUKS volume management. Open, Close and Status commands are managed through luksctl script.

OneDataCtl
----------
Reads Onedata ini file, usually stored on ``/etc/galaxy/onedatactl.ini``, for Onedata space management: both user data and reference data.

mount_space
***********
To mount onedata space (userdata or refdata), call:

::

    onedata = OneDataCtl('/etc/galaxy/onedatactl.ini', 'userdata')
    onedata.mount_space()

umount_space
************
To umount onedata space, call:

::

    onedata = OneDataCtl('/etc/galaxy/onedatactl.ini', 'userdata')
    onedata.umount_space()
