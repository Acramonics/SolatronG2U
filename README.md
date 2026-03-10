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

A video on GPIB (also known as IEEE-488) is at
https://www.youtube.com/watch?v=EEtETGfL_VE

The original circuit and software was by Rudolf Reuter and modified by
@TheHWCave. Rudolf's blog, where this was described, doesn't seem to
be available any more (as of March 2026), but @TheHWCave provides a
detailed description of the circuit on YouTube at
https://www.youtube.com/watch?v=RaLirRvSngk (see the screenshots in
the `SourceImages` directory).  He builds it on stripboard and uses an
Arduino breakout board, so I decided to create a PCB instead. He was
unable to obtain a PCB-mounted Centronics-style (*Series 57*) 24-pin
connector. These are now easily available from AliExpress (at about
£2.50 with free postage if you spend more than £8.00), and I have used
a PCB-mounted male connector that can plug straight into the back of
the hardware, so you don't need to worry about cables.

@TheHWCave provides the code for the Arduino Nano 3 and a logger script at
https://github.com/TheHWcave/GPIB-to-USB

He provides an update video at
https://www.youtube.com/watch?v=DAS1KVU_FaA which explains how to
address a problem with the Arduino losing its software when the USB us
disconnected, but the GPIB connection is still present. The GPIB seems
to provide some partial power to the Arduino and he provides
instructions on setting a brownout fuse in software.

I provide a summary of all the necessary information on this page.

Note that there is also discussion of creaing a GPIB/USB interface at
https://egirland.blogspot.com/2014/03/arduino-uno-as-usb-to-gpib-controller.html
Note that this uses different pin assignments and different software.

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
In this application, this is rather irrelevant as everything is
connected to a common ground.

Software
--------

You will need the software available from
https://github.com/TheHWcave/GPIB-to-USB

Using this is explained in the video at
https://www.youtube.com/watch?v=RaLirRvSngk

The 'brownout fuse' setting is described in the video at
https://www.youtube.com/watch?v=DAS1KVU_FaA I will provide
instructions when I have verified this on a couple of Arduino Nano
boards.

