# Intel Aero board LEDs

There's a multicolor LED on top of the board (if the board is in the enclosure, you can see the light from the white cable hole), and an orange LED under the board. As the LEDs are enclosed in the Ready-To-Fly design, it is not very useful. But if you build your own drone design or enclosing you may want to let the LEDs visible and use them. To install the IO module:

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

# CAN

The Intel Aero Compute Board includes a MCP2515 CAN controller and MCP2562 CAN transceiver. The controller is connected to the Atom processor via the SPI interface on bus 1 (SPI1) chip select 0 (CS0). It can be accessed via spidev as /dev/spidev1.0. [Python spidev libraries](https://github.com/doceme/py-spidev)
