# AR488-build

Build of AR488 using Arduino Pro Micro & artag firmware.

![PCBs](PCBs.jpg)

Main repo: https://github.com/Twilight-Logic/AR488

Gerbers: https://www.eevblog.com/forum/projects/ar488-arduino-based-gpib-adapter/msg3362552/#msg3362552

(Mirrored in this repo)

Firmware: https://github.com/Twilight-Logic/AR488/tree/master/Contributed/artag

(Mirrored in this repo)

## Parts

Amazon: "Pro Micro Atmega32U4 5V 16MHz Bootloadered IDE Micro USB Pro Micro Development Board Microcontroller Compatible with Pro Micro Serial Connection with Pin Header"

SCSI plug: 111-024-113L001

## Download firmware

Using Arduino IDE (tested on 1.8.7)

Select "Arduino/Genuino Micro" as the board and short the RST/GND pins briefly during upload.

## Keithley 617

Commands to talk interfactively using Putty (115200 baud)

```
++verbose
++addr 29
++auto 1
F0X
F1X
```

F0X and F1X should generate some response from the device.

Command reference:

```
Function (F) - F0 (Volts) F1 (Amps) F2 (Ohms) F3 (Coulombs) F4 (External Feedback) F5 V/I Ohms
Range (R) - R0 to R12 (see manual)
Zero Check (C) - C0/C1
Zero Correct (Z) - Z0/Z1
Suppress (N) - N0/N1
Trigger (T)
Voltage Source Operate (O) - O0/O1
Read Mode (B) - B0 to B4 (see manual)
Display Mode (D)
Data Storage (Q)
SRQ Mode (M)
EOI and Bus Hold-off (K)
Terminator (Y)
[Other commands in the manual such as voltage source value, data store mode, calibration]
```

Useful commands:

```
ClXZlXC0X - Zero check on, zero correct, zero check off
```
