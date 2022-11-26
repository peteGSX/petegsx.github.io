********************
Generic Control Knob
********************

In the generic control knob mode, an OLED displays both the last position sent to the EX-CommandStation in addition to the currently selected knob position.

A single button press will send the current knob position to the EX-CommandStation.

Valid positions are from -127 to 127 as a single byte is used to send this value over I2C.

Hardware details
================

.. image:: /_static/images/rotary-encoder/rotary-encoder.png
  :alt: Rotary Encoder Fritzing
  :scale: 40%

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

