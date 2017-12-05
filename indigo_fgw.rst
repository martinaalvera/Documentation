INDIGO FutureGateway
====================

To correctly setup the FGW portal follow the instruction in the ``Ubuntu LTS 14.04 Server`` section here: https://indigo-dc.gitbooks.io/futuregateway/content/installation.html

The ssh port is, usually, the ``22``.

Portal configuration
--------------------

Start the portal:

::

  # /etc/init.d/futuregateway start

The portal will available at http(s)://<your_ip_address>:8080

.. Note::

   FGW (re)start take a while!

Login with the mail configured during the wizard and ``test`` as password. Then set your new password and recovery question.

Apache configuration
--------------------

Enalble http_proxy on apache2

::

  a2enmod proxy_http

In ``/etc/apach2/sites-available/`` create your `futuregateway.conf <https://raw.githubusercontent.com/mtangaro/fgw-elixir-italy/master/configs/futuregateway.conf>`_ file, setting

::

  ServerName <your_serve_name>

  ...

then enable FGW:

::

  a2dissite futuregateway.conf

and reload apache:

::

  # service apache2 reload

Enable https
------------

Enalble http_proxy and ssl modules on apache2

::

  a2enmod ssl
  a2enmod proxy_http

Port ``443`` must be opened.

In ``/etc/apach2/sites-available/`` create your `futuregateway.conf <https://raw.githubusercontent.com/mtangaro/fgw-elixir-italy/master/configs/futuregateway.ssl.conf>`_ file, setting

::

  ServerName <your_serve_name>

  ...

  ## SSL directives
  SSLEngine on
  SSLCertificateFile /path/to/cert.pem
  SSLCertificateKeyFile /path/to/key.pem
  SSLCertificateChainFile /path/to/chain.pem

  ...

then enable FGW:

::

  a2dissite futuregateway.conf

and reload apache:

::

  # service apache2 reload

Add to FGW configuration file ``portal-ext.properties`` the following lines:

::

  web.server.protocol=https
  web.server.https.port=443

and restart FGW:

::

  # /etc/init.d/futuregateway restart

To create your signed cetificate with Let's Encrypt: https://github.com/maricaantonacci/slam/blob/master/gitbook/create-custom-keystore.md

IAM integration
---------------

Iam portlets for the FGW portal are available on github: https://github.com/mtangaro/fgw-elixir-italy/tree/master/iam-modules

You can follow this instructions to set it up: https://github.com/indigo-dc/LiferayPlugIns/blob/master/doc/admin.md. The deploy directory is in ``/home/futuregateway/FutureGateway/deploy/``.

The option ``javascript.fast.load=false`` has to be set in ``/home/futuregateway/FutureGateway/portal-ext.properties``.

Administrator portlet
---------------------

The administrator portlet is here: https://github.com/mtangaro/fgw-elixir-italy/tree/master/admin-modules

Galaxy portlet
--------------

Build FGW portlets
******************

Create build environment
------------------------

To correctly build FutureGateway portlets we recommends to use ``Ubuntu 16.04``
``Java 8`` and ``gradle`` are needed:

::

  # apt-get install gradle

Install Blade cli: https://dev.liferay.com/develop/tutorials/-/knowledge_base/7-0/installing-blade-cli

The linux version of the liferay portal is available here: https://sourceforge.net/projects/lportal/files/Liferay%20Workspace/1.5.0.1/LiferayWorkspace-1.5.0.1-linux-x64-installer.run

::

  $ chmod +x LiferayWorkspace-1.5.0.1-linux-x64-installer.run

  $ ./LiferayWorkspace-1.5.0.1-linux-x64-installer.run

Answer ``[2] Don't initialize Liferay Workspace directory``

and continue the installation.

Build portlets
--------------

Next you should use some code lines like below:

::

  blade init liferay-workspace

  cd ./liferay-workspace

  git clone https://github.com/indigo-dc/LiferayPlugIns modules/

  cd ./modules

  git checkout remotes/origin/nonofficial # to build nonofficial portlets

  blade gw clean jar

Newly created portlets are in ./modules/LIB_NAME/build/libs.

Next you need copy created jars to ~/FutureGateway/deploy and portlets are available on the your website.

References
**********

GitBook: https://www.gitbook.com/book/indigo-dc/futuregateway/details
