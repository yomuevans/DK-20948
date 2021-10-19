# DK-20948
The ICM20948/SAMG55 Dev Kit is compatible with the Atmel’s ATSAMG55-XPRO evaluation kit based on a SAM G55 Cortex™- M4 processor-based microcontrollers. The supported development tools are Atmel Studio and Embedded Debugger. The purpose of this solution is to allow sensor management and algorithm processing by using a standalone microcontroller. The ICM20948/SAMG55 solution is an embedded sensors combo (accelerometer &amp; gyroscope &amp; magnetometer) on chip, easy to integrate for users developing within the wearable and IoT space. 

# HARDWARE PLATFORM
The TDK Dev Kit platform for ICM20948 consists of the following components:
- TDK SAMG55 Dev Kit with onboard ICM20948
- ICM20948 contains AK09916 based Magnetometer (a.k.a. AKM9916)
ATSAMG55-XPRO SETUP
The TDK SAMG55 Dev Kit includes a SAMG55J19A microcontroller. For more information on this MCU, please refer to Atmel
website (see Useful Links section above.)

# ATSAMG55 BOARD SETUP
The systems pictured above are configured for I2C communication between the ATSAMG55 and the ICM20948.
Jumper configurations -
- Power (J1)
o To power the Dev Kit via the EDBG USB port (J500), connect a jumper across pins 3 & 4.
o To receive power via the FTDI USB port (CN6), connect a jumper across pins 5 & 6 (default).
Note: The second configuration (power over the FTDI port) is useful when the firmware has already been flashed and no
debugging is required. This configuration allows only for only one USB connection, via the FTDI port.
- I2C/SPI configuration (J2)
o For communication between the ATSAMG55 and the ICM20948 via I2C, add jumpers between pins 1 & 2 and
pins 3 & 4.
o For communication between the ATSAMG55 and the ICM20948 via SPI, remove the jumpers between pins 1 &
2 and pins 3 & 4.
Note: By default, the firmware and hardware are setup for I2C communication. To use the SPI interface, both the
hardware (as described above) and the firmware (as described below) must be changed.
- UART (J3)

For UART communication over FTDI, connect pins 1 & 2 and pins 3 & 4.
- AKM9916 based Magnetometer
o The Magnetometer is inbuilt and no external jumper connection is required to access the compass.
2.2.1 Powering the SAMG55 Dev Kit
To power the platform, connect either the J500 or the CN6 port (based on the J1 jumper setting) to a PC using a micro-USB
cable.
2.2.2 Debugging on the SAMG55 Dev Kit
To debug or flash the firmware, the EDBG USB port needs to be connected to a host PC using a micro-USB cable. There is also a
provision for the firmware to print debug traces on the EDBG UART/USB connector. AtmelStudio Terminal Window can be used
to read the messages at baud-rate 921600 by selecting the correct COM port. The serial line configurations are mentioned
below. In order to disable data logging across the UART, the INV_MSG_ENABLE macro must be undefined and the firmware
rebuilt. If the verbose level needs to be changed, the INV_MSG_ENABLE macro needs to be overloaded with the new desired
verbose level.

# SOFTWARE ENVIRONMENT
# PREREQUISITE
To build and use the samples application provided as part for the DK-20948 Developer Kit packages, the following software is
required:
- An RS232 terminal emulator (such as Putty: http://www.putty.org/)
o To retrieve traces from provided FW application
- Atmel Studio: http://www.atmel.com/tools/atmelstudio.aspx
o To load FW binaries and access to the USB EDBG port of the SAMG55 Dev Kit
