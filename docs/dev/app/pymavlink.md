# Hello World in PyMAVLink

[PyMAVLink](https://github.com/ArduPilot/pymavlink) is a Python library for handling MAVLink protocol streams and log files. This allows for the creation of simple scripts to analyse telemetry logs from autopilots which use the MAVLink protocol. Here's a simple python script using the basic pymavlink wrapper to arm the motors for 3 seconds. Arming the motors is the simplest action we can test to show everything is connected.

!!! Note
    It is advised to unplug propellers before running this code.

```python
#!/usr/bin/python
from __future__ import print_function

import pymavlink.mavutil as mavutil
import sys

mav = mavutil.mavlink_connection('tcp:127.0.0.1:5760')
mav.wait_heartbeat()
mav.mav.command_long_send(mav.target_system, mav.target_component,
                          mavutil.mavlink.MAV_CMD_COMPONENT_ARM_DISARM, 0, 1,
                                                    0, 0, 0, 0, 0, 0)
sleep(3)
mav.mav.command_long_send(mav.target_system, mav.target_component,
                          mavutil.mavlink.MAV_CMD_COMPONENT_ARM_DISARM, 0, 0,
                          0, 0, 0, 0, 0, 0)
```
Some more examples which uses pymavlink can be found [here](https://github.com/01org/mavlink-router/tree/master/examples).
