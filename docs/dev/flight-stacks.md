# Flightstack Development

Intel® Aero Platform supports both PX4 and ArduPilot flight stacks, the former being the default from factory. Here we give an overview on the steps necessary to customize flight stack.

## PX4

Latest PX4 middleware can be downloaded from [here](https://github.com/PX4/Firmware). Detailed development guide is documented [here](https://dev.px4.io/en/).
Any new modules or sample applications that are developed have to be added in cmake file present in below path,
```console
cmake/configs/nuttx_aerofc-v1_default.cmake
```
Connect Aero board to development system using USB cable and compile PX4 Firmware with below command which will also flash the updated firmware on Intel-Aero,
```console
# make aerofc-v1_default upload
```

## ArduPilot

Latest ArduPilot Firmware can be downloaded from [here](https://github.com/ArduPilot/ardupilot). Detailed development guide is documented [here](http://ardupilot.org/dev/).
Connect Aero board to development system using USB cable and run below commands to compile and upload the Firmware on to Intel-Aero,
```console
# ./waf configure --board aerofc-v1 
# ./waf --target bin/arducopter --upload
```
