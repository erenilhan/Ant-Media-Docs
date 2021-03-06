The one-time token method is one of the effective authentication methods
to secure your streams. Ant Media Server offers one-time token security
control option with 1.5.0 version.

The Parameters of the Token
~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  TokenId: Generated a random string from service.
-  StreamId: The Id of the resource that user wants to reach.
-  ExpireDate: The expiration date of the token.
-  Type: Either ``publish`` or ``play`` token.

Enable Setting
~~~~~~~~~~~~~~

Firstly, the setting should be enabled in the management panel.

.. figure:: https://i0.wp.com/antmedia.io/wp-content/uploads/2018/09/Screenshot-from-2018-09-17-20-53-01-1024x441.png
   :alt: token setting

   token setting

The Steps for Token Control Mechanism
-------------------------------------

A) Publishing Scenario
~~~~~~~~~~~~~~~~~~~~~~

Step 1. Create a Token
^^^^^^^^^^^^^^^^^^^^^^

The Server creates tokens with
`getToken <https://github.com/ant-media/Ant-Media-Server/blob/14e243dd8f1696fbbc66b582eadbbe301e516e72/src/main/java/io/antmedia/rest/BroadcastRestService.java#L976>`__
Rest Service getting streamId, expireDate and type parameters with query
parameters. Service returns tokenId and other parameters. It is
important that streamId and type parameters should be defined properly.
Because tokenId needs to match with both streamId and type.

The sample token creation service URL:

``http://[IP_Address]:5080/<Application_Name>/rest/broadcast/getToken?id=<Stream_Id>&expireDate=<Expire_Date>&type=publish``

Please note that calling this rest service from remote is restricted due
to the security reasons.

If you want to remove this filtering mechanism please remove the below
lines from webapps-> {Application} -> WEBINF -> web.xml

.. code:: xml

   <filter>
       <filter-name>RestAuthenticationFiler</filter-name>
       <filter-class>io.antmedia.serverapp.pscp.filter.RestAuthenticationFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>RestAuthenticationFiler</filter-name>
       <url-pattern>/rest/*</url-pattern>
   </filter-mapping>

Step 2. Request with Token
^^^^^^^^^^^^^^^^^^^^^^^^^^

The system controls token validity during publishing or playing.

**RTMP Publishing:** You need to add a token parameter to RTMP URL
before publishing. Sample URL:

``rtmp://[IP_Address]/<Application_Name>/<Stream_Id>?token=tokenId``

**WebRTC Publishing:** Token parameter should be inserted to publish
WebSocket message.

.. code:: json

   {
       command : "publish",
       streamId : "stream1",
       token : "tokenId",
   }

For details about WebRTC WebSocket messaging please visit `wiki
page <https://github.com/ant-media/Ant-Media-Server/wiki/WebRTC-WebSocket-Messaging-Details>`__.

B) Playing Scenario
~~~~~~~~~~~~~~~~~~~

.. _step-1.-create-a-token-1:

Step 1. Create a Token
^^^^^^^^^^^^^^^^^^^^^^

The Server creates tokens with
`getToken <https://github.com/ant-media/Ant-Media-Server/blob/14e243dd8f1696fbbc66b582eadbbe301e516e72/src/main/java/io/antmedia/rest/BroadcastRestService.java#L976>`__
Rest Service getting streamId, expireDate and type parameters with query
parameters. Service returns tokenId and other parameters. It is
important that streamId and type parameters should be defined properly.
Because tokenId needs to match with both streamId and type.

The sample token creation service URL:
``http://[IP_Address]:5080/<Application_Name>/rest/broadcast/getToken?id=<Stream_Id>&expireDate=<Expire_Date>&type=play``

Please note that calling this rest service from remote is restricted due
to the security reasons.

If you want to remove this filtering mechanism please remove the below
lines from webapps-> {Application} -> WEBINF -> web.xml

.. code:: xml

   <filter>
       <filter-name>RestAuthenticationFiler</filter-name>
       <filter-class>io.antmedia.serverapp.pscp.filter.RestAuthenticationFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>RestAuthenticationFiler</filter-name>
       <url-pattern>/rest/*</url-pattern>
   </filter-mapping>

.. _step-2.-request-with-token-1:

Step 2. Request with Token
^^^^^^^^^^^^^^^^^^^^^^^^^^

**Live Stream/VoD Playing:** Same as publishing, the token parameter is
added to URL. Sample URL:

``http://[IP_Address]/<Application_Name>/streams/<Stream_Id_or_Source_Name>?token=tokenId``

**WebRTC Playing:** Again the token parameter should be inserted to play
WebSocket message.

.. code:: json

   {
       command : "play",
       streamId : "stream1",
       token : "tokenId",

   }

Please have a look at the principles described in the `wiki
page <https://github.com/ant-media/Ant-Media-Server/wiki/WebRTC-WebSocket-Messaging-Details>`__.

Evaluation of the Token
~~~~~~~~~~~~~~~~~~~~~~~

Ant Media Server evaluates based on its properties to secure your
streams. Whether it is valid for the requested stream or not is
controlled. Another important control process is checking the type of
the token. Because the developer or administrator may give access to a
user to play a stream but not publish to this stream even with the same
streamId.

Once the token is successfully validated by Ant Media Server, then it is
removed from the database so that other requests with the same token
will be dismissed. Since consecutive requests are sent during
playing/accessing streams, the session information saved after the
one-time token is consumed. \**\*
