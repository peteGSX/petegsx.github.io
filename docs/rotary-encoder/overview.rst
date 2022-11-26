*********************
DCC-EX Rotary Encoder
*********************

.. warning:: 

  This code is very much in Alpha testing, functionality may change at any time, and much testing is needed. For bugs or feedback, refer to :doc:`/contact`.

This software has been written to enable an Arduino with a rotary encoder connected to it to be integrated with a DCC-EX CommandStation.

The primary purpose is to select a position for a turntable via EX-RAIL automation, however it could be used for other purposes.

There are currently two different ways that this encoder can be used, with either option being suitable for use in a mimic panel:

1. As a generic control knob with a standard, SPI connected monochrome OLED display to select a position between -127 and 127.
2. As a specific turntable controller utilising an SPI connected GC9A01 round colour LCD display to select predefined positions.

.. note:: 

  One other option tested was to use the rotary encoder with a pointer type knob (without a display) to select positions printed directly on a mimic panel. However, rotating the knob to specific positions has proven unreliable and this idea has been abandoned. It's possible that it relates to the quality of rotary encoder used or the way the software has been written, so if anyone else is interested in testing/implementing this feature then you are more than welcome to do so, and if you wish, you can `get in contact with me <contact>`_. I have left the code intact that allows re-aligning the encoder with a specific "home" position (see :ref:`rotary-encoder/overview:usage` below).

.. toctree:: 
  :hidden:
  :maxdepth: 1

  control-knob
  turntable-controller
  ex-rail-integration

Software requirements
=====================

In order to use this with a DCC-EX CommandStation, it must be running the "rotary-encoder" branch of EX-CommandStation which is based on the current development branch:

`EX-CommandStation rotary-encoder branch <https://github.com/DCC-EX/CommandStation-EX/tree/rotary-encoder>`_

Hardware requirements
=====================

This requires an AVR based Arduino (tested on a Nano), a rotary encoder (tested with a KY-040), and an SPI connected OLED or GC9A01 round LCD display.

See the relevant :doc:`/rotary-encoder/control-knob` or :doc:`/rotary-encoder/turntable-controller` page for hardware and connection details.

Obviously, a suitable DCC-EX EX-CommandStation must be available, with the rotary encoder Arduino connected to it via I2C.

Refer to the `DCC-EX documentation <https://dcc-ex.com>`_ for further information on EX-CommandStation.

Installation and configuration
==============================

The provided config.example.h in addition to the Fritzing diagrams included on the relevant pages should help identify the correct pins to connect the encoder and display to.

Refer to the relevant pages for the various configuration options available.

The default I2C address for this device is 0x80, and you will need to enable the device driver via myHal.cpp.

Example:

.. code-block:: cpp
  
  #include "IO_RotaryEncoder.h"

  void halSetup() {
    RotaryEncoder::create(700, 1, 0x80);
  }

Usage
=====

Once the software has been configured and uploaded to the rotary encoder Arduino, and your EX-CommandStation has been configured to support it with the updated software uploaded, you can simply rotate the encoder to the appropriate position desired, and a push of the button will send that position to the EX-CommandStation.

In the generic control knob mode, it will send a position between -127 and 127. The OLED will display the last selected position in addition to the position reflected by the current knob position.

In turntable controller mode, the knob rotates a representative turntable on the GC9A01 round LCD, and will send the predefined position number when pushing the encoder button. Pushing the button with the representative turntable in any other position will not update the EX-CommandStation. 

As per the introductory note at the top of this page, functionality has been retained to rotate the knob back to a "home" position. This is accomplished by holding the button down for a second then releasing it, resulting in the OLED display indicating it can now be re-homed. Simply rotate the encoder to the desired home or 0 position, then press the button once to confirm. Normal functionality will then resume. This only applies to the generic control knob mode, and is not available in turntable controller mode.