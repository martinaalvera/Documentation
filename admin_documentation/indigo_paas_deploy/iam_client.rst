Create IAM client or protected resource
---------------------------------------

#. Login as administrator or registered user.

#. Click on **MitreID Dashboard** and then **Self-service client registration** for client creation or **Self-service protected resource registration** to register a new protected resource.

#. Click on *New client* and provides at least the the following parameters:

   ::

     Client name = iam-client-name

     redirect URI(s) = http(s)://<service_url>

   .. warning::

      The redirect URI(s) is required only for client creation.

#. Configure your client as requested by your service, for example:

   ::

     Scopes: openid, profile, email, address, phone, offline_access
       
     Grant Types: authorization code, refresh

#. Save the client ID, client secret and registration access token (needed to modify the client).

.. figure:: _static/mitre.png
   :scale: 25%
   :align: center

.. centered:: Fig.3: The MitreID Dashboard

 
.. figure:: _static/client_conf.png
   :scale: 25%
   :align: center

.. centered:: Fig.4: MitreID Dashboard client registration
