# AR488-build

Build of AR488 using Arduino Pro Micro & artag firmware.

Main repo: https://github.com/Twilight-Logic/AR488

Gerbers: https://www.eevblog.com/forum/projects/ar488-arduino-based-gpib-adapter/msg3362552/#msg3362552

Firmware: https://github.com/Twilight-Logic/AR488/tree/master/Contributed/artag

## Parts

Amazon: "Pro Micro Atmega32U4 5V 16MHz Bootloadered IDE Micro USB Pro Micro Development Board Microcontroller Compatible with Pro Micro Serial Connection with Pin Header"

SCSI plug: 111-024-113L001

## Download firmware

Select "Arduino/Genuino Micro" as the board and short the RST/GND pins briefly during upload.

## Keithley 617

Commands to talk interfactively using Putty (115200 baud)

```
++verbose
++addr 29
++auto 1
F0
F1
```

F0 and F1 should generate some response from the device.
