# AR488-build

Build of AR488 using Arduino Pro Micro & artag firmware.

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