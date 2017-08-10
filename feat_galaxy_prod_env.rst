Galaxy production environment
=============================
The system allows to setup and launch a virtual machine (VM) configured with the Operative System (CentOS 7 or Ubuntu 14.04/16.04) and the auxiliary applications needed to support a Galaxy production environment such as PostgreSQL, Nginx, uWSGI and Proftpd and to deploy the Galaxy platform itself. A common set of Reference data is available through a CernVM-FS volume.

Once deployed each Galaxy instance can be further customized with tools and reference data.

THe Galaxy production environment is deployed according to Galaxy official documentation: https://galaxyproject.org/admin/config/performance/production-serverr

.. _fig_updateprocess:
according to :: _static/galaxy_prod_env.png
   :scale: 100 %
   :align: center
   :alt: galaxy production environment

OS support
----------
CentOS 7 is our default distribution, Given its adherence to Standards and the length of official support (CentOS-7 updates until June 30, 2024, https://wiki.centos.org/FAQ/General#head-fe8a0be91ee3e7dea812e8694491e1dde5b75e6d). CentOS 7 and Ubuntu (14.04 and 16.04) are both supported.

CentOS 7 and Ubuntu Xenial 16.04 exploit systemd as as init system, while Ubuntu Trusty 14.04 still uses upstart.

PostgresSQL
-----------
PostgreSQL packages coming from PostgreSQL official repository are installed:

==============  ===============
Distribution	Repository
==============  ===============
Centos		https://wiki.postgresql.org/wiki/YUM_Installation
Ubuntu		https://wiki.postgresql.org/wiki/Apt
==============  ===============

Current stable PostgreSQL version is installed: ``PostgreSQL 9.6``

On CentOS 7 the default pgdata directory is ``/var/lib/pgsql/9.6/data``. The ``pg_hba.conf`` configuration is modified allowing for password authentication. On CentOS we need to exclude CentOS base and updates repo for PostgreSQL, otherwise dependencies might resolve to the postgresql supplied by the base repository.

On Ubuntu default pgdata directory is ``/var/lib/postgresql/9.6/main``, while the configuration files are stored in ``/etc/postgresql/9.6/main``. There's no need to modify the HBA configuration file since, by default, it is allowing password authentication.

PostgreSQL start/stop/status in entrusted to Systemd on CentOS 7 and Ubuntu Xenial and to Upstart for Ubuntu Trusty.

==============	=================
Distribution	Command
==============  =================
CentOS 7	sudo systemctl start/stop/status postgres-9.6
Ubuntu Xenial	sudo systemctl start/stop/status postgresql
Ubuntu Trusty	sudo service postgresql start/stop/status
==============  =================

Galaxy database configuration
****************************
Two different database are configured to track data and tool shed install data, allowing to bootstrap fresh Galaxy instance with pretested installs.
The database passwords are randomly generated and the passoword can be retrieved in the ``galaxy.ini`` file.
 
Galaxy database is named ``galaxy`` and is configured in the ``galaxy.ini`` file:

::

  database_connection = postgresql://galaxy:gtLxNnH7DpISmI5FXeeI@localhost:5432/galaxy


The shed install tool database is named ``galaxy_tools`` and is configured as:

::

  install_database_connection = postgresql://galaxy:gtLxNnH7DpISmI5FXeeI@localhost:5432/galaxy_tools

Docker
******
On Docker container PostgreSQL cannot be managed through systemd/upstart, since there's no init system on CentOS and Ubuntu docker images.
Therefore, the system is automatically configured to run postgresql using ``supervisord``.

NGINX
-----
To improve Galaxy performance, NGINX is used as web server. The official Galaxy nginx packages are used by default (built in upload module support).

==============  ===============
Distribution    Repository
==============  ===============
Centos          https://depot.galaxyproject.org/yum/
Ubuntu          ppa:galaxyproject/nginx
==============  ===============

Moreover, on Ubuntu, we need to prevent NGINX to be updated by apt default packages. For this purpose the pin priority of NGINX ppa packages is raised, by editing ``/etc/apt/preferences.d/galaxyproject-nginx-pin-700`` (more on apt pinning at: https://wiki.debian.org/AptPreferences).

NGINX is configured following the official Galaxy wiki: https://galaxyproject.org/admin/config/nginx-proxy/.

Finally, to start/stop/status NGINX:

==============  =================
Dstribution     Command
==============  =================
CentOS 7        sudo systemctl start/stop/status nginx
Ubuntu Xenial   sudo systemctl start/stop/status nginx
Ubuntu Trusty   sudo service nginx start/stop/status 
==============  =================

uWSGI
-----

Proftpd
-------

Supervisord
-----------

Init scripts
------------
