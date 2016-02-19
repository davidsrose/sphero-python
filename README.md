# sphero-python

Some tools for Bluetooth LE based Orbotix things like Ollie and BB8.
Tested with Orbotix Ollie.

These are some tools to handle the so-called user hack mode, which is just a serial shell you can activate using an API command.

First set `deviceAddress` in **BB8_driver.py** (see original README on the bottom).

Enabling User Hack Mode
-----------------------

To enable UHM (only needed one time):
```
% ./userhackmode.py
```

If everything works correctly (I had to shutdown bluetoothd as it seems to block the BT device), and your Bluetooth device is in proximity to your Orbotix gadget, it should connect, blink its RGB LED and then activate stuff.

To disable UHM, type 'uhd' in user hack shell or look at the source of `userhackmode.py`.

User Hack Shell
---------------

**userhackshell.py** is an interactive `python-cmd` based shell to probe around in UHM.

Commands:
```
help - shows internal commands
connect - Connect to your BLE device. You need to be close to it to activate.
disconnect - well...
quit - disconnect and quit shell
log - activate dumping following output of stdout to logfile.log
flash - blink RGB LED red, green, blue, off
quote <value> - send value directly to device. useful for "quote help"

All other commands get send to the device.
```

Usage example:

```
% ./userhackshell.py
Orbotix User Hack Shell
(Cmd) connect
Connecting ...
Sending antidos
Sending txpower
Sending wakecpu
OK

(Cmd) quote help
You are in a maze of twisty little passages, all alike...

(Cmd) ver
Module Versions:
Bootloader = 5.6
Main App   = 5.49
Board Rev  = 1
OrbBasic   = 1.7
Macro Exec = 6
Config Block = 116
Chassis ID=1
MA CRC-32 = 0x240CEDB1

(Cmd) br
Board Rev = 1

(Cmd) st
Sensors healthy, Bluetooth and Auth chip OK

(Cmd) pd
PID preset = 2
Gains
Pitch P=20.000 I=0.100 D=700.000
Roll  P=21.000 I=0.300 D=50.000
Yaw   P=30.000 I=0.015 D=2500.000

(Cmd) vd
Low voltage   = 360
Crit voltage  = 350
ADC intercept = -0.006732
ADC slope     = 0.001139
Curr voltage  = 4.050000

(Cmd) vd
Low voltage   = 360
Crit voltage  = 350
ADC intercept = -0.006732
ADC slope     = 0.001139
Curr voltage  = 4.050000

(Cmd) vp1
Battery State = BATT_OK, Battery Voltage = 405, Battery Voltage = 4.050000, ADC=3574.000000

(Cmd) vp1
Battery State = BATT_OK, Battery Voltage = 405, Battery Voltage = 4.050000, ADC=3582.000000

(Cmd) vp2
Real T Voltage=4.060000, RT  PWM Throttled=4095
Low RT Voltage=4.050000, Low PWM Throttled=4095

(Cmd) vp2
Real T Voltage=4.050000, RT  PWM Throttled=4095
Low RT Voltage=4.050000, Low PWM Throttled=4095

(Cmd) da 1
Accel debug on
(Cmd) do 1
Orientation debug on
(Cmd) dv 1
Voltage debug on
Battery State = BATT_OK, Battery Voltage = 405, Battery Voltage = 4.050000, ADC=3581.000000
IMU: p=-10.7737 r=5.3267 y=-0.3882 timeS=0.002508
Accel: X=0.0952 Y=0.1904 Z=1.0147 one=1.036817
Battery State = BATT_OK, Battery Voltage = 405, Battery Voltage = 4.050000, ADC=3582.000000
IMU: p=-10.7789 r=5.3445 y=-0.3854 timeS=0.002507
Accel: X=0.0953 Y=0.1983 Z=1.0147 one=1.038311
Battery State = BATT_OK, Battery Voltage = 405, Battery Voltage = 4.050000, ADC=3582.000000
IMU: p=-10.7748 r=5.3448 y=-0.3791 timeS=0.002498
Accel: X=0.0913 Y=0.1984 Z=1.0109 one=1.034240
...

(Cmd) dz
All debug off

(Cmd) quit
Disconnecting ...
```

Dependencies
------------

bluepy: https://github.com/IanHarvey/bluepy

References
----------

Forked from: https://github.com/jchadwhite/SpheroBB8-python

Which is based on: https://gist.github.com/ali1234/5e5758d9c591090291d6

SpheroBB8-python README
-----------------------

**Sphero's BB8 droid** 
*The droid you've been looking for.*

Now even better with a python API library!

Use "sudo hcitool lescan" to find BB8's MAC address 
input it at "`deviceAddress =`" (line 244) in the Sphero class in BB8_driver.py

**

***Included Scripts:***

**
**BB8Test.py**
A simple program that connects to BB8 and flashes the internal RGB LED red to green to blue. You can take it a step further and add `bb8.roll` commands to make him move using the API. 

**BB8joyDrive.py**
*requires PyGame library* 

Allow you to drive BB8 with a joystick/gamepad.
Shows on screen feedback of analog stick as well as speed and heading
Currently setup for a Xbox 360 controller.

 - Left analog stick controls BB8's movement, much the like app!   
 - Holding the Left trigger stops BB8.
 - Tapping the Left bumper changes BB8's heading - used to calibration.   
 -  Holding the Right bumper turns on BB8's blue 'tail light' to aid in calibration.

> Adapted the sphero driver library from:
> https://github.com/mmwise/sphero_ros/tree/groovy-devel/sphero_driver/src/sphero_driver
> 
> Used the bluetooth 'stuff' from:
> https://gist.github.com/ali1234/5e5758d9c591090291d6

**TODO:**
Tie in the btle handleNotifcations to Sphero response API
    

 - getting sensor info, command responses, etc. back from BB8

