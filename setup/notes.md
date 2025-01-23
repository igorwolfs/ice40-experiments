# Flashing the ice40-h8k FPGA

### Connection attempt - Blue-pill
There's a great tool around to turn the blue-pill board into an SPI-flasher.
```bash
git clone https://github.com/ivanovp/blue_flash.git
```

Clone the repo, and flash the binary onto the blue-pill (e.g.: through UART on pin PA9, PA10 using the stm32cube-programmer).

### Pin connections for the iCE40HX8K-EVB board
- [connection on olimex-board] -> [connection on blue-pill board]
- SPI_CS / SPI_NSS -> PA4
- SPI_MISO -> PA6
- SPI_MOSI -> PA7
- SPI_SCK -> PA5
- CRESET -> PA3
- CDONE -> PA2
- GND -> GND

- WP, HOLD: should be pulled to Vcc.
    - They both are already pulled-up with a 10 kOhm resistor

NOTE: pin 1 on the olimex-connector starts closest to the power-jack away from the board edge.

### Output
For some reason I get this output when connecting:

```bash
Compiled on Mar 20 2018 19:16:22
Watchdog disabled
+++ printf test! +++
Connect USB device (enable 1.5k pull-up resistor on D+)

SFDP header
===========
Signature: 0x50444653
Version: 1.6
Number of parameter headers: 2
#0 parameter header
--------------------
ID MSB: 0xFF
ID LSB: 0x00
Type: Basic SPI protocol
Version: 1.6
Length: 9 DW
Table pointer: 0x000030
3-byte only addressing
Density: 2097152 bytes
Sector size: 4096 bytes, erase opcode: 0x20
Sector size: 32768 bytes, erase opcode: 0x52
Sector size: 65536 bytes, erase opcode: 0xD8
Selected sector size: 65536 bytes, erase opcode: 0xD8
Enter 4-byte addressing: 0xFF

#1 parameter header
--------------------
ID MSB: 0xFF
ID LSB: 0xEB
flash_read_parameter_header:318 ERROR: Unknown parameter header ID LSB: 0xEB!


Flash initialized
DFU flash descriptor: @SPI Flash (ID 0xBA6015, Size: 2097152 bytes)/0x00000000/32*064Kg
Flash de-initialized
Release CRESET
SPI deinitialized
GPIO pins released
Set CRESET
Release CRESET
```

I did however, not add any extra pull-ups, since the WP/HOLD pins are already pulled-up to Vcc with 10 kOhm.

### Connection attempt - FT232H breakout board

