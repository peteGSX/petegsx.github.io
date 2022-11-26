********************
Turntable Controller
********************

In the turntable controller mode, a GC9A01 round LCD displays a representative turntable with each pre-defined position around a representative turntable pit.

A single button press will send the current knob position to the EX-CommandStation.

Valid positions are from -127 to 127 as a single byte is used to send this value over I2C.

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

