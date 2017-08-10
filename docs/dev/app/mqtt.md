# Drone communication using MQTT

This section provides sample application which communicates with Intel Aero though MQTT.

### Prerequisites
* Python MQTT API on Intel Aero
```console
# pip install paho-mqtt
```
* [MQTT client for browser](https://chrome.google.com/webstore/detail/mqttlens/hemojaaeigabkbcookmlgmdigohjobjm?hl=en)

!!! Note
    It is advised to unplug propellers before running this code.

Below is the client code running on Intel Aero,
```python
#!/usr/bin/python
import paho.mqtt.client as mqtt
from dronekit import connect, VehicleMode, LocationGlobalRelative
import time
vehicle = connect('tcp:127.0.0.1:5760', wait_ready=True)
vehicle.mode    = VehicleMode("GUIDED")
print("Flight Controller Connected")

def on_connect(client, userdata, rc):
    print("Client connected ")
    client.subscribe("aero-paul")
def on_message(client, userdata, msg):
    print("Arming motors ("+msg.topic+"/"+str(msg.payload)+")")
    vehicle.armed   = True                                   
    while not vehicle.armed:                                 
        time.sleep(1)                           
    time.sleep(5)                                   
    print("Disarming")                            
    vehicle.armed   = False                       
client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message
client.connect("test.mosquitto.org", 1883, 60)
client.loop_forever()
```
