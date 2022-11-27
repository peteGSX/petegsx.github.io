********************
Turntable Controller
********************

In turntable controller mode, a GC9A01 round LCD displays a representative turntable with each pre-defined position indicated around a representative turntable pit.

Rotating the rotary encoder will rotate the representative turntable in either a clockwise or anti-clockwise direction.

When the representative turntable's home end aligns with either the home position or any of the predefined turntable positions, the textual description of the position will be displayed, and the home end of the representative turntable will be highlighted.

When aligned in this manner, a single button press will send the predefined position's ID to the EX-CommandStation.

Position definitions
--------------------

"positions.example.h"

Valid position IDs are from 0 to 255, however 0 is representative of the "home" position, so it is recommended not to use this for any other position.

Defining colours
----------------

"colours.example.h"

Predefined colours are located in "Arduino_GFX.h", and you can define any colour you choose by specifying the appropriate hex value eg. 0x0000 is black, and 0xFFFF is white.

Hardware details
================

`Waveshare <https://www.waveshare.com/1.28inch-LCD-Module.htm>`_

`Waveshare Wiki <https://www.waveshare.com/wiki/1.28inch_LCD_Module>`_

.. image:: /_static/images/rotary-encoder/rotary-encoder-gc9a01.png
  :alt: Rotary Encoder Fritzing
  :scale: 90%

A suitable rotary encoder (tested on KY-040) and SPI OLED connected to a suitable AVR based Arduino (tested on a Nano) is all that's required for the generic control knob functionality, with the Arduino connected to your EX-CommandStation via I2C as outlined in the Fritzing diagram.

Configuration options
=====================

General options
---------------

I2C Address - default 0x80
Mode - default TURNTABLE_MODE
Diagnostics - default commented out

Rotary encoder options
----------------------

HALF_STEP


Display options
---------------

