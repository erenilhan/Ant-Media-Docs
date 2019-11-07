General Steps How to Create Own WebRTC Conference Room and Peer to Peer
---------------------------
This guide describes How to Create Own WebRTC Conference Room and Peer to Peer with Ant Media Server. This guide you can use WebRTC solutions in different communication formations. In addition to peer-to-peer (1-1)  and publish-play (1-N) communication types, you can also implement a WebRTC conference (N-N) solution with Ant Media Server Javascript SDK. Also, WebRTC latency is average 0.5 seconds. Let’s have a look at that step by step. 

How to Create Own WebRTC Conference Room
--------------------------------

At the end of this tutorial, you have basic WebRTC Conference Room. This tutorial scope is basics in WebRTC Conference Room. For the detailed technical information follow this `link <https://antmedia.io/how-to-create-a-webrtc-conference-room/>`_.

 You need some requirements in build Conference Room. Requirements in listed in below.

.. tip::

	Requeirements

	-Ant Media Server Enterprise Edition

	-SSL both of Website & Ant Media Server

Firstly, you need Ant Media Server Enterprise Edition in this solution. Also, you need SSL in your Website & Ant Media Server. Because of Google Chrome Security rules. If you haven't got any domain for your Ant Media Server, you can get free domain in Freenom.

 
Step 1. Prepare the Ant Media Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We recommended for Ant Media Server in Ubuntu 16.04. Ant Media Server installation is easy and basic. You can install Ant Media Server in follow `this <https://github.com/ant-media/Ant-Media-Server/wiki/Getting-Started/>`_. tutorial. Also, you need SSL for the Ant Media Server. So, you have to need domain for your Ant Media Server.

If everything is OK, then we skip to the next step.

Step 2. Prepare the HTML Page 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In this section you need some css & js in HTML pages. 

Include JavaScript files to your page in the header as follows.

.. code-block:: java

	<head> 
	<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
	<script src="https://github.com/ant-media/StreamApp/blob/master/src/main/webapp/js/webrtc_adaptor.js"></script> 
	</head>


Include Body some tags to your page in the body as follows.

.. code-block:: java

	...
	<div class="jumbotron">
	<div id="players">
	<div class="col-sm-3">
	<video id="localVideo" autoplay muted></video>
	</div>
	</div>

	<div class="row">
	<div class="col-sm-6 col-sm-offset-3">
	<p>
	<input type="text" class="form-control" value="room1" id="roomName" placeholder="Type room name">
	</p>
	<p>
	<button onclick="joinRoom()" class="btn btn-info" disabled id="join_publish_button">Join Room</button>
	<button onclick="leaveRoom()" class="btn btn-info" disabled id="stop_publish_button">Leave Room</button>
	</p>

	<span class="label label-success" id="broadcastingInfo"
	style="font-size: 14px; display: none" style="display: none">Publishing</span>
	</div>
	</div>
	...


Include footer some codes to your page in the body as follows.

.. code-block:: java

	Define Media source variable, SDP variable and etc. 

	Define websocketURL your URL.
	var websocketURL = "wss://domain-name.com:5443/WebRTCAppEE/websocket";

	var webRTCAdaptor = new WebRTCAdaptor(

	}


You can analyze and follow the `Conference Example <https://antmedia.io/livedemo/conference.html>`_ in the Live Demo also.

We hope this tutorial will give an idea about WebRTC conference applications. You can analyze the example at the `Test Server <https://test.antmedia.io:5443/WebRTCAppEE/conference.html>`_. If you have a question, please let us know through contact@antmedia.io

How to Create Own WebRTC Peer to Peer Communication
--------------------------------

At the end of this tutorial, you have basic WebRTC Peer to Peer Communication. This tutorial scope is basics in WebRTC Peer to Peer Communication. For the detailed technical information follow this `link <https://antmedia.io/how-to-create-webrtc-peer-to-peer-communication/>`_.

You need some requirements in build Peer to Peer Communication. Requirements in listed in below.

.. tip::

	Requeirements
	-Ant Media Server Enterprise Edition
	-SSL both of Website & Ant Media Server

	...

Firstly, you need Ant Media Server Enterprise Edition in this solution. Also, you need SSL in your Website & Ant Media Server. Because of Google Chrome Security rules. If you haven't got any domain for your Ant Media Server, you can get free domain in Freenom.

 
Step 1. Prepare the Ant Media Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We recommended for Ant Media Server in Ubuntu 16.04. Ant Media Server installation is easy and basic. You can install Ant Media Server in follow `this <https://github.com/ant-media/Ant-Media-Server/wiki/Getting-Started/>`_. tutorial. Also, you need SSL for the Ant Media Server. So, you have to need domain for your Ant Media Server.

If everything is OK, then we skip to the next step.

Step 2. Prepare the HTML Page 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In this section you need some css & js in HTML pages. 

Include JavaScript files to your page in the header as follows.

.. code-block:: java

	<head> 
	<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
	<script src="https://github.com/ant-media/StreamApp/blob/master/src/main/webapp/js/webrtc_adaptor.js"></script> 
	</head>

Include Body some codes to your page in the body as follows.

.. code-block:: java

	...
	<video id="localVideo" autoplay muted width="480"></video>
	<video id="remoteVideo" autoplay controls width="480"></video>
	<br /> <br />
	<div class="input-group col-sm-offset-2 col-sm-8">
	<input type="text" class="form-control" value="stream1" id="streamName" placeholder="Type stream name"> <span class="input-group-btn">
	<button onclick="join()" class="btn btn-default" disabled id="join_button">Join</button>
	<button onclick="leave()" class="btn btn-default" disabled id="leave_button">Leave</button>
	</span>
	</div>
	<div style="padding:10px">
	<button onclick="turnOffLocalCamera()" class="btn btn-default"  >Turn off Camera</button>
	<button onclick="turnOnLocalCamera()" class="btn btn-default"  >Turn on Camera</button>
	
	<button onclick="muteLocalMic()" class="btn btn-default"  >Mute Local Mic</button>
	<button onclick="unmuteLocalMic()" class="btn btn-default"  >Unmute Local Mic</button>	
	</div>
	...

Include footer some codes to your page in the body as follows.

.. code-block:: java

	...
	Define Media Source variable, SDP variable and etc. 
	
	Define websocketURL your URL.
	var websocketURL = "wss://domain-name.com:5443/WebRTCAppEE/websocket";

	var webRTCAdaptor = new WebRTCAdaptor(
	
	}
	...


You can analyze and follow the `Peer to Peer Example <https://antmedia.io/livedemo/peer.html>`_ in the Live Demo also.

We hope this tutorial will give an idea about WebRTC conference applications. You can analyze the example at the `Test Server <https://test.antmedia.io:5443/WebRTCAppEE/peer.html>`_. If you have a question, please let us know through contact@antmedia.io