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

![DK-20948](https://github.com/yomuevans/DK-20948/blob/main/Images/eMD_Software_Guide_ICM20948.jpg?raw=true)

# SOFTWARE ENVIRONMENT
# PREREQUISITE
To build and use the samples application provided as part for the DK-20948 Developer Kit packages, the following software is
required:
- An RS232 terminal emulator (such as Putty: http://www.putty.org/)
o To retrieve traces from provided FW application
- Atmel Studio: http://www.atmel.com/tools/atmelstudio.aspx
o To load FW binaries and access to the USB EDBG port of the SAMG55 Dev Kit


# EMD DEVELOPER KIT TDK PACKAGES
The following package is available:
- eMD-SmartMotion_ICM20948_x.y.z.zip
This example targets low performance microcontrollers with a very simple sensor application.
Tools running on the PC for data display are available within the delivered package.

# FW PACKAGE DESCRIPTION
The DK-20948 package includes all the necessary files to create a custom application using an ICM20948 device.
The package is organized as follow
- doc: Document(s) describing the use of this firmware development platform.
- EMD-App: contains sample firmware source and project files.
  - src:
    - At the top level: Shared .c & .h files.
    - ASF: Shared Atmel system files.
    - config: Shared config files.
    - ICM*: Sensor specific files, main.[c,h], sensor.[c,h] and system.[c,h].
* *.cproj: AtmelStudio project files for each of the supported sensors.
- EMD-Core: Contains TDK driver files. These files are built into an archive libEMD-Core-ICM*.a. Each supported sensor
has it’s own .a file.
* config : The Makefiles used to create the sensor driver archives.
* sources/Invn: TDK libraries source files.
* *.cproj: AtmelStudio project files for each of the supported sensors.
- scripts – Batch files for building and flashing release versions of the firmware for each sensor.
- tools – The files required to run the host application sensor-cli.
- EMD-G55-ICM*.atsln – Atmel Studio solution files for each of the supported sensors.
- release – contains precompiled elf and binary files


# BUILDING AND RUNNING SAMPLES APPLICATIONS
# OVERVIEW
The following two projects are available:

 EMD-App – This application project demonstrates how to use TDK-InvenSense’s low-level drivers to control and retrieve
data from ICM devices. It encodes sensor events and sends them over the UART interface to be displayed by sensor-cli. The
application uses the Core library and Algo libraries to generate a loadable binary.

 EMD-Core – This project includes low-level drivers and firmware code and generates the eMD Core library used by the
EMD-APP.

# Choosing between SPI and I2C
By default, I2C is used to communicate between ATSAMG55 and ICM device. This can be changed to SPI by setting #define
USE_SPI_NOT_I2C define to 1 (can be found in system.h) and by removing the jumpers between pins 1 & 2 and pins 3 and 4 of
J2 (as described above).
Note: 20x48 SPI slave interface speed should not be set higher than 2.5MHz to ensure sensor data consistency

Configuring the device
Full Scale Range (FSR) can be changed by updating the value of the corresponding variables in sensor.c.
Default FSR value are +/- 4g for accelerometer and +/- 2000dps for gyroscope.

Supported FSR values are:

Gyroscope:

* The variable to modify is: cfg_gyr_fsr.
* 250dps, 500dps, 1000dps and 2000dps

 Accelerometer:
* The variable to modify is: cfg_acc_fsr.
* 2g, 4g, 8g and 16g

Note: Accelerometer FSR is expressed in mg in the driver stack and application.
The array cfg_mounting_matrix (for acc and gyro) is defined in sensor.c. Modifying the elements of the arrays will reconfigure
the mounting matrix for the associated sensors.
Default mounting matrix is set to identity which corresponds to the following reference frame:

Supported sensor features
- Raw accelerometer
- Raw Gyroscope
- Calibrated accelerometer
- Calibrated gyroscope
- Uncalibrated gyroscope
- Game rotation vector
- Gravity
- Linear Acceleration
Optional sensor features supported:
- Calibrated magnetometer (Inbuilt AKM9916 only)
- Uncalibrated magnetometer
- Rotation vector
- Geomagnetic rotation vector
- Step Detector
- Step Counter
- Tilt Detector
- Pick-up Gesture
- BAC (Activity Classifier)
- B2S
- SMD
