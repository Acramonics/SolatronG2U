G2U
===

Andrew Martin, acramonics, 2026
-------------------------------

`G2U` is a PCB for a GPIB to USB adapter using an Arduino Nano 3.

GPIB is a vendor-neutral interface for controlling equipment and
logging data. While rather outdated, and largely replaced by USB and
Ethernet, some equipment still uses it and there are many second hand
devices (such as multimeters) that use it including the well-regarded
Solartron 7150+.

A video on GPIB (also known as IEEE-488) is on
[YouTube](https://www.youtube.com/watch?v=EEtETGfL_VE) and details are
on [Wikipedia](https://en.wikipedia.org/wiki/GPIB).

The original circuit and software was by Rudolf Reuter and modified by
@TheHWCave. Rudolf's blog, where this was described, doesn't seem to
be available any more (as of March 2026), but @TheHWCave provides a
detailed description of the circuit on
[YouTube](https://www.youtube.com/watch?v=RaLirRvSngk) (see the
screenshots in the `SourceImages` directory).  He builds it on
stripboard and uses an Arduino breakout board, so I decided to create
a PCB instead. He was unable to obtain a PCB-mounted Centronics-style
(*Series 57*) 24-pin connector. These are now easily available from
AliExpress (at about £2.50 with free postage if you spend more than
£8.00), and I have used a PCB-mounted male connector that can plug
straight into the back of the hardware, so you don't need to worry
about cables.

Software
--------

@TheHWCave provides the code for the Arduino Nano 3 and a logger
script on [GitHub](https://github.com/TheHWcave/GPIB-to-USB).

He provides an [update
video](https://www.youtube.com/watch?v=DAS1KVU_FaA) which explains how
to address a problem with the Arduino losing its software when the USB
us disconnected, but the GPIB connection is still present. The GPIB
seems to provide some partial power to the Arduino and he provides
instructions on setting a brownout fuse in software.

I provide a summary of all the necessary information on this page.

Note that there is also [discussion of creating a GPIB/USB
interface](https://egirland.blogspot.com/2014/03/arduino-uno-as-usb-to-gpib-controller.html),
but note that this uses different pin assignments and different
software.

The PCB
-------

As is often the case with my PCBs, you will require my
`ACRM_KiCad_Libs` to provide the footprint for the 24-pin male
Centronics-style connector.

Bill of Materials
-----------------

- Arduino Nano 3.x with USB (ideally USB-C) [1 off]
- 6K2 0.25W resistors (R1-R16) [16 off]
- 120R 0.25W resistors (R17-R32) [16 off]
- Centronics-style 24P 'Series 57' male connector [1 off]

The PCB is 78.05mm x 71.40mm so you will need a plastic case to
accomodate this.  The Centronics-style connector projects from the
board so will need a suitable cutout. The USB connector is set back on
the board, so it's not easy to plug a cable in and out once the board
is in the case, but, since the GPIB sockets are usually at the back of
equipment, the expectation is that the board and the cable will be
left plugged in.

Ardunio to GPIB connections
---------------------------

This table is expanded from a table shown in @TheHWCave's video (see
the screenshot in the `SourceImages` directory) and shows which
connections from the Arduino go to which pins on the GPIB. The Arduino
pins are shown with the pin number (from 1-30) and the position on the
left (L) or right (R) column of pins - both counting from the top.

| Arduino Line | Arduino Pin |     | GPIB Pin | Function | ATMega328P          |
|--------------|-------------|-----|----------|----------|---------------------|
| A0           | 19/R12      | --- | 1        | DIO1     | (PC0/ADC0)          |
| A1           | 20/R11      | --- | 2        | DIO2     | (CP1/ADC1)          |
| A2           | 21/R10      | --- | 3        | DIO3     | (PC2/ADC2)          |
| A3           | 22/R9       | --- | 4        | DIO4     | (PC3/ADC3)          |
| A4           | 23/R8       | --- | 13       | DIO5     | (PC4/ADC4)          |
| A5           | 24/R7       | --- | 14       | DIO6     | (PC5/ADC5)          |
| D10          | 13/L13      | --- | 15       | DIO7     | (PB2)               |
| D11          | 14/L14      | --- | 16       | DIO8     | (PB3(MOSI))         |
| D8           | 11/L11      | --- | 5        | EIO      | (PB0)               |
| D7           | 10/L10      | --- | 6        | DAV      | (PD7)               |
| D6           |  9/L9       | --- | 7        | NRFD     | (PD6)               |
| D5           |  8/L8       | --- | 8        | NDAC     | (PD5)               |
| D4           |  7/L7       | --- | 9        | IFC      | (PD4)               |
| D3           |  6/L6       | --- | 10       | SRQ      | (PD3)               |
| D2           |  5/L5       | --- | 11       | ATN      | (PD2)               |
| D9           | 12/L12      | --- | 17       | REN      | (PB1)               |
| GND          |  4/L4       | --- | 12,18-24 | GND      |                     |
| GND          | 29/R2       | --- | 12,18-24 | GND      |                     |
| +5V          | 27/R4       | +5V |          |          |                     |
| D1/TX1       |  1/L1       | NC  |          |          |                     |
| RX0          |  2/L2       | NC  |          |          |                     |
| RESET        |  3/L3       | NC  |          |          |                     |
| D12          | 15/L15      | NC  |          |          |                     |
| VIN          | 30/R1       | NC  |          |          |                     |
| RESET2       | 28/R3       | NC  |          |          |                     |
| A7           | 26/R5       | NC  |          |          |                     |
| A6           | 25/R6       | NC  |          |          |                     |
| AREF         | 18/R13      | NC  |          |          |                     |
| +3V3         | 17/R14      | NC  |          |          |                     |
| D13          | 16/R15      | NC  |          |          |                     |

Note that each GND pin in the GPIB connector is paired with one of the
data lines in a twisted pair. Pin 12 is connected to the cable shield.
See [GPIB on WikiPedia](https://en.wikipedia.org/wiki/GPIB). In this
application, this is rather irrelevant as everything is connected to a
common ground.

Software
--------

You will need the software available from
https://github.com/TheHWcave/GPIB-to-USB

Using this is explained in the video at
https://www.youtube.com/watch?v=RaLirRvSngk

The 'brownout fuse' setting is described in the video at
https://www.youtube.com/watch?v=DAS1KVU_FaA 

Software installation steps
---------------------------

### Installing the Arduino software

*To be written.*

### Setting the brownout fuse

*I will write a more detailed version when I have verified this on a
couple of Arduino Nano boards. This is largely in note form!*


Set the extended fuse byte

Extended Fuse Byte | Bit No | Description | Default Value
-------------------|--------|-------------|--------------
-                  | 7      | -           | 1
-                  | 6      | -           | 1
-                  | 5      | -           | 1
-                  | 4      | -           | 1
-                  | 3      | -           | 1
BODLEVEL2          | 2      | (*)         | 1 (unset)
BODLEVEL1          | 1      | (*)         | 1 (unset)
BODLEVEL0          | 0      | (*)         | 1 (unset)

(*) Brown-out Detector trigger level

BODLEVEL 2:0 Fuses | Min V    | Typ V    | Max V    | Units
-------------------|----------|----------|----------|------
111                | Off      | Off      | Off      |
110                | 1.7      | 1.8      | 2.0      | V
101                | 2.5      | 2.7      | 2.9      | V
100                | 4.1      | 4.3      | 4.5      | V
011                | Reserved | Reserved | Reserved |
010                | Reserved | Reserved | Reserved |
001                | Reserved | Reserved | Reserved |
000                | Reserved | Reserved | Reserved |

BODLEVEL 2.0 Fuse setting b100 (#04) for 4.1V cutoff
By default it is set to #FF

Need a second Arduino or an ICSP programmer spported by the Arduino
IDE to set the fuse. The AVRDude software is used to run the
programmer. 

Different Arduinos use different chips which have different signature
bytes and this needs to match the programmer:

Chip        | Byte 0x000 | Byte 0x001 | Byte 0x002
------------|------------|------------|------------
ATmega328   | 0x1E       | 0x95       | 0x14
ATmega328P  | 0x1E       | 0x95       | 0x0F
ATmega328PB | 0x1E       | 0x95       | 0x16

For example, the Arduino IDE may call AVRDude expecting to find an
ATmega328P, but AVRDude finds an ATmega328PB and stops.

If this happens, simply copy the failed command from the upload window
and run it from the command line instead correcting the errornous chip
type. For example, assuming the arduino IDE is installed in a
directory pointed to by the environment variable `$ARDUINO`:

```
$ARDUINO/hardware/tools/avr/bin/avrdude \
   -C$ARDUINO/hardware/tools/avr/etc/avrdude.cong \
   -v -patmega328p \
   -cusbasp -Pusb -e -Ulock:w:0x3F:m -Uefuse:w:0xF4:m \
   -Uhfuse:w:0xDA:m -Ulfuse:w:0xFF:m
```
becomes
```
$ARDUINO/hardware/tools/avr/bin/avrdude \
   -C$ARDUINO/hardware/tools/avr/etc/avrdude.cong \
   -v -patmega328pb \
   -cusbasp -Pusb -e -Ulock:w:0x3F:m -Uefuse:w:0xF4:m \
   -Uhfuse:w:0xDA:m -Ulfuse:w:0xFF:m
```
(Note the change in the 3rd line)

If your IDE isinstalled in `$HOME/arduino-1.8.9`, then you would type
```
export ARDUINO=$HOME/arduino-1.8.9
```
before running the above command.

Alternatively, if using Linux, Create file `~/.avrduderc` containing:
```
part parent "m328"
    id			= "m328p";
    desc		= "ATmega328P";
    signature		= 0x1e 0x95 0x14;

    ocdrev              = 1;
;
```
(setting the `desc` and `signature` as required).




This erases the memory so, you then need to restore the bootloader:
```
~/arduino-1.8.9/hardware/tools/avr/bin/avrdude \
   -C~/arduino-1.8.9/hardware/tools/avr/etc/avrdude.cong \
   -v -patmega328pb \
   -cusbasp -Pusb -Uflash:w:./optiboot_atmega328.hex
```
(This also allows the latest bootloader to be downloaded and installed.)

You can then remove the in-circuit programmer and upload the
GPIB-to-USB software sketch in the normal way from the Arduino IDE
through the USB cable and with the newly installed boot loader.


Future plans
------------

In future, I may do an SMD version to minimize the size and weight!

