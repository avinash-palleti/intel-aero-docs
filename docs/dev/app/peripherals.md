# Intel Aero board LEDs

There's a multicolor LED on top of the board (if the board is in the enclosure, you can see the light from the white cable hole), and an orange LED under the board. As the LEDs are enclosed in the Ready-To-Fly design, it is not very useful. But if you build your own drone design or enclosing you may want to let the LEDs visible and use them.
To install IO module on Intel Aero,
```console
# pip install python-periphery
```
Below is the sample code to test all LED colors,
```python
#!/usr/bin/python
import time
from periphery import GPIO

print "Top LED Blue"
gpio = GPIO(403, "out")
gpio.write(bool(1))
time.sleep(1)
gpio.write(bool(0))
gpio.close()

print "Top LED Green"
gpio = GPIO(397, "out")
gpio.write(bool(1))
time.sleep(1)
gpio.write(bool(0))
gpio.close()

print "Top LED Red"
gpio = GPIO(437, "out")
gpio.write(bool(1))
time.sleep(1)
gpio.write(bool(0))
gpio.close()

print "Bottom LED Orange"
gpio = GPIO(507, "out")
gpio.write(bool(1))
time.sleep(1)
gpio.write(bool(0))
gpio.close()
```

You can find sample shell script which programs LED colors at below path on Intel Aero board
```console
# vi /usr/bin/aero-led-ctrl
```
!!! Warning
    These LEDs are used by system components to notify about the current state.
