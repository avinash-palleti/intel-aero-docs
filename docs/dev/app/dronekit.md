# Hello World in Dronekit

It’s important to know the basics of [mavlink](https://mavlink.io/en/), as it is the base of all communications with the Flight Controllers. [Dronekit](python.dronekit.io) is an abstraction on top of mavlink to make it very user friendly. To install on Intel Aero:

```console
# pip install dronekit
```

!!! Note
    It is advised to unplug the propellers before running below code.

Below is the sample code which makes use of DroneKit and arm the motors and disarm after 5s.

```python
#!/usr/bin/python
from dronekit import connect, VehicleMode, LocationGlobalRelative
import time

vehicle = connect('tcp:127.0.0.1:5760', wait_ready=True)
print "Arming motors:"
vehicle.mode    = VehicleMode("GUIDED")
vehicle.armed   = True
while not vehicle.armed:
    print "  Waiting for arming to be finished"
    time.sleep(1)
print "Keeping motors armed for 5s"
time.sleep(5)
print "Disarming"
vehicle.armed   = False
```
Some more examples using Dronekit can be found [here](http://python.dronekit.io/examples/)
