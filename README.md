Nano code and Logger script:
https://github.com/TheHWcave/GPIB-to-USB

Discussion:
https://egirland.blogspot.com/2014/03/arduino-uno-as-usb-to-gpib-controller.html

Video on making an adapter and using the interface
https://www.youtube.com/watch?v=RaLirRvSngk

Update to video
https://www.youtube.com/watch?v=DAS1KVU_FaA


| Arduino Line | Arduino Pin | GPIB Pin | Function | ATMega328P     |
|---------|-------------|----------|----------|---------------------|
| A0      | 19/R12      | 1        | DIO1     | (PC0/ADC0)          |
| A1      | 20/R11      | 2        | DIO2     | (CP1/ADC1)          |
| A2      | 21/R10      | 3        | DIO3     | (PC2/ADC2)          |
| A3      | 22/R9       | 4        | DIO4     | (PC3/ADC3)          |
| A4      | 23/R8       | 13       | DIO5     | (PC4/ADC4)          |
| A5      | 24/R7       | 14       | DIO6     | (PC5/ADC5)          |
| D10     | 13/L13      | 15       | DIO7     | (PB2)               |
| D11     | 14/L14      | 16       | DIO8     | (PB3(MOSI))         |
| D8      | 11/L11      | 5        | EIO      | (PB0)               |
| D7      | 10/L10      | 6        | DAV      | (PD7)               |
| D6      |  9/L9       | 7        | NRFD     | (PD6)               |
| D5      |  8/L8       | 8        | NDAC     | (PD5)               |
| D4      |  7/L7       | 9        | IFC      | (PD4)               |
| D3      |  6/L6       | 10       | SRQ      | (PD3)               |
| D2      |  5/L5       | 11       | ATN      | (PD2)               |
| D9      | 12/L12      | 17       | REN      | (PB1)               |
| GND     |  4/L4       | 12,18-24 | GND      | 12 to cable shield  |
| D1/TX1  |  1/L1       | NC       |          |                     |
| RX0     |  2/L2       | NC       |          |                     |
| RESET   |  3/L3       | NC       |          |                     |
| D12     | 15/L15      | NC       |          |                     |
| VIN     | 30/R1       | NC       |          |                     |
| GND     | 29/R2       | GND      | GND      |                     |
| RESET2  | 28/R3       | NC       |          |                     |
| +5V     | 27/R4       | +5V      |          |                     |
| A7      | 26/R5       | NC       |          |                     |
| A6      | 25/R6       | NC       |          |                     |
| AREF    | 18/R13      | NC       |          |                     |
| +3V3    | 17/R14      | NC       |          |                     |
| D13     | 16/R15      | NC       |          |                     |



