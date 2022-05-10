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
Function (F) - F0 (Volts) F1 (Amps) F2 (Ohms) F3 (Coulombs) F4 (External Feedback) F5 (V/I Ohms)
Range (R) - R0 to R12 (see manual 3-19)
Zero Check (C) - C0/C1
Zero Correct (Z) - Z0/Z1
Suppress (N) - N0/N1
Trigger (T) - T0 to T7 (see manual 3-20)
Voltage Source Operate (O) - O0/O1
Read Mode (B) - B0 to B4 (see manual 3-19)
Display Mode (D) - D0/D1 (Electrometer/Voltage Source)
Data Storage (Q) - Q0 to Q7 (see manual 3-19)
SRQ Mode (M) - M0 to M32 (see manual 3-20)
EOI and Bus Hold-off (K) - K0 to K3 (see manual 3-20)
Terminator (Y) (see manual 3-20)
[Some other commands in manual]
```

Useful commands:

```
C1XZ1XC0X - Zero check on, zero correct, zero check off
```

### Code

```
var devices = SerialDevices.Browse();
if (devices.Count == 0)
    Console.WriteLine("\tNone");
string gpib = "";
foreach (var device in devices)
{
    Console.WriteLine($"\t{device.InstanceName} - {device.PortName}");
    if (device.PortName.Contains("Arduino Micro"))
        gpib = device.InstanceName;
}

if (gpib == "")
    Console.WriteLine("Did not find serial device");
else
{
    var k617 = new SerialConnection(gpib, new SerialSettings(115200));
    k617.Write("++addr 29\n");
    k617.Write("++auto 0\n");
    k617.Write("C1XZ1XC0X\n");
    k617.Write("T5F1R0N0D0B0Q7O0G1X\n");
    k617.Write("++auto 1\n");

    while (!Console.KeyAvailable)
    {
        k617.Write("X\n");
        if (k617.TryReadBytes(3000, out var data))
        {
            Console.WriteLine(Encoding.ASCII.GetString(data));
        }
    }
}
```
