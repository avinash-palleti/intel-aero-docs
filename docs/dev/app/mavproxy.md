# Hello World in PyMAVProxy

On top of being a developer friendly layer on top of MAVLINK, MAVProxy was designed to bridge the gap between programming-only libraries like DroneKit and graphical-only tools like QGroundControl. Check: [ardupilot.github.io/MAVProxy](http://ardupilot.github.io/MAVProxy/html/index.html) Some people use it on a remote computer to control the drone and have optional user interfaces to complex functions, but you an use on the drone itself for autonomous drone development. To install on Intel Aero:

```console
# pip install mavproxy
```
!!! Note
    It is advised to unplug propellers before running this code.

Launch the shell,
```console
# mavproxy.py --master=tcp:127.0.0.1:5760 --quadcopter
```
And type a few commands to arm/disarm the motors:
```console
# arm throttle
# disarm
# bat
```

