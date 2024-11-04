***************************
DCC-EX Turntable Controller
***************************

This is a controller for DCC-EX turntables, operating as a native DCC-EX protocol client to utilise a turntable object and allow a user to operate it.

Turntable operations are displayed on a round LCD, with a rotary encoder utilised for user input.

It is capable of operating any type of turntable configured using the new DCC-EX turntable object, including both EX-Turntable and DCC turntables.

Information on the new turntable object is available on the `DCC-EX website <https://dcc-ex.com/ex-commandstation/accessories/turntables/index.html>`_.

A future version may implement support for a WiFi client connection to the DCC-EX CommandStation rather than needing a physical serial connection.

How it works (and DCC-EX turntable configuration)
=================================================

When creating a turntable object in DCC-EX EX-CommandStation, you can specify an angle for each position, which is what this DCC-EX Turntable Controller software uses to configure the turntable display.

The angle of the home position is taken from what would be 12 o'clock on a traditional clock face (the top centre of the circle), with each position's angle taken from the home position in a clockwise direction.

If you do not specify an angle when creating a turntable object, this software will be unable to correctly render each position on screen.

Operation
---------

When the software starts, it will retrieve the first configured turntable object from the EX-CommandStation, and display the various positions on screen, with the turntable bridge represented at the current position of the turntable object.

To operate the turntable, simply rotate the rotary encoder to the desired position, and a single click of the encoder's button will send the selection to the CommandStation.

If the turntable is configured as an EX-Turntable, the display will flash the bridge and position name while the turntable is moving. As there is no feedback from DCC turntables, this will not happen with those.

To select the home position (again, only valid for EX-Turntable), either select it using the rotary encoder and click the button, or just double click it.

Holding down the rotary encoder's button will reset the DCC-EX Turntable Controller.

Software
========

The software for the turntable controller is available in my `DCC-EX Turntable Controller <https://github.com/peteGSX-Projects/DCCEXTurntableController>`_ GitHub repository.

Installation
------------

The repository is setup to enable PlatformIO to be used with VSCode and will automatically install the required libraries:

- DCC-EX/DCCEXProtocol
- bodmer/TFT_eSPI
- avandalen/Switch

The platformio.ini file is written to configure the TFT_eSPI library correctly according to the :ref:`dcc-ex-turntable-controller/index:pins and connections` section below, meaning manual configuration of the TFT_eSPI library shouldn't be required.

If you prefer, you can also use the Arduino IDE, which means you will need to:

- Install the above libraries
- Configure the TFT_eSPI manually according to the [library's documentation](https://github.com/Bodmer/TFT_eSPI)

There is plenty of information and tutorials available to help with VSCode, PlatformIO, the Arduino IDE, and libraries, so I will not cover that here.

Configuration
-------------

To get up and running, just uploading the software to the Blackpill and connecting the display, rotary encoder, and serial connection should simply work "out of the box".

If you wish to customise the colours and font in use, you can copy the included "myConfig.example.h" to "myConfig.h" and edit it to suit. Instructions are in the file.

Hardware requirements
=====================

To assemble the DCC-EX Turntable Controller, you will need:

- An STM32F411CEU6 Blackpill microcontroller
- A rotary encoder such as the KY-040
- A GC9A01 based round LCD

Further to this, you will need a serial connection to a DCC-EX CommandStation.

Pins and connections
--------------------

The below pins are used on the Blackpill to connect to the CommandStation's serial port, rotary encoder, and GC9A01 LCD.

Remember to cross Rx/Tx so that the Blackpill Rx connects to the CommandStation's Tx, and vice versa. Also be sure to connect a common ground, and take into account if the CommandStation uses 3.3V or 5V logic, as the Blackpill is a 3.3V uC.

- Serial Rx - PA10
- Serial Tx - PA9
- Rotary encoder button - PB15
- Rotary encoder DT - PB14
- Rotary encoder CLK - PB13
- GC9A01 DIN - PA7
- GC9A01 CLK - PA5
- GC9A01 CS - PA4
- GC9A01 DC - PA3
- GC9A01 RST - PA2
- GC9A01 BL - PA1
