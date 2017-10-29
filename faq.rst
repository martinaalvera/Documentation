Frequently Asked Questions
==========================
Questions that apply to	Galaxy instances.

Reboot Galaxy instance
----------------------
How to correctly restart Galaxy after Virtual Machine reboot?

#. PostgreSQL is already running

#. Proftpd is aready running

#. Start NGINX: ``sudo nginx``

   Now connecting to you IP address, you should see:

   .. figure:: _static/faq/faq_restart_galaxy_1.png
      :scale: 25 %
      :align: center
      :alt: NGINX default page

   while conneting to your galaxy instance you should see:

   .. figure:: _static/faq/faq_restart_galaxy_2.png
      :scale: 25 %
      :align: center
      :alt: Galaxy page

#. Finally, to correctly start all Galaxy services run: ``sudo /usr/local/bin/galaxy-startup``

   ::

     $ sudo /usr/local/bin/galaxy-startup 
     Loading Galaxy environment
     Starting the Galaxy production environment
     Galaxy start: [ OK ] 

   .. figure:: _static/faq/faq_restart_galaxy_3.png
      :scale: 25 %
      :align: center
      :alt: Galaxy page
