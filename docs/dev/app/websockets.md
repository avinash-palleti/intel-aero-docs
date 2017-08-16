# Drone communication using WebSockets

This section provides sample application which communicates with Intel Aero though websockets.

### Prerequisites
* Python websocket API on Intel Aero
```console
# pip install websocket-server
```
* [WebSocket client for browser](https://chrome.google.com/webstore/detail/smart-websocket-client/omalebghpgejjiaoknljcfmglgbpocdp)
* Optionally, a Library on your development station to send the request from a script instead of your browser:
```
# pip install websocket-client
```

!!! Note
    It is advised to unplug propellers before running this code.

Below is the server code that runs on Aero,
```python
#!/usr/bin/python
from websocket_server import WebsocketServer
import re
from dronekit import connect, VehicleMode, LocationGlobalRelative
import time
vehicle = connect('tcp:127.0.0.1:5760', wait_ready=True)
vehicle.mode    = VehicleMode("GUIDED")
print("Flight Controller Connected")
def new_client(client, server):
    print("Client connected")
    server.send_message_to_all("Client connected")
def message_received(client, server, message):
    if len(message) > 200:
        message = message[:200]+'..'
    print("Arming motors")
    vehicle.armed   = True
    while not vehicle.armed:
        time.sleep(1)
    time.sleep(5)
    print("Disarming")
    vehicle.armed   = False
    server = WebsocketServer(8080, '0.0.0.0')
    server.set_fn_new_client(new_client)
    server.set_fn_message_received(message_received)
    server.run_forever()
```
Below is the optional client code, running on a remote computer (change the 
IP 192.168.0.100 with Aero's IP on your network):
```python
#!/usr/bin/python
from websocket import create_connection
ws = create_connection("ws://192.168.0.100:8080")
ws.send("Alert, send drone")
result = ws.recv()
print("Received '%s'" % result)
ws.close()
```
Some more examples which uses websockets can be found [here](https://github.com/01org/mavlink-router/tree/master/examples).
