*******************
Software and Logic
*******************

As mentioned in the overview, this code is heavily based on the turntable example provided with the NmraDcc Arduino library, and this library is what provides the DCC accessory decoder functionality.

In addition, the AccelStepper library is used to provide acceleration and deceleration for the turntable for somewhat prototypical operation.

You can find the code in my `GitHub repo <https://github.com/peteGSX-Projects/programmable-dcc-turntable>`_.

Startup
========

On startup, the decoder address is read from the EEPROM along with the various position definitions that have been programmed, and these are all printed to the serial port.

The DCC decoder object is initialised in order to respond to DCC packets received via the interrupt pin.

The stepper motor is homed, then rotated to the defined position 1.

In action
==========

Once startup is complete, both the DCC decoder and stepper motor objects are processed regularly to ensure correct operation.

The DCC decoder object will respond to all DCC accessory notifications as such:

When a notification is received, compare the provided address with the defined number of positions in CV 513.
If it's one of the defined positions, is different to the last position moved to, and the stepper is not still moving, proceed.
Read the position definitions as stored in the appropriate CVs for the number of steps to move to, and the polarity.
Calculate the steps required to move to the new position from the last position, including calculating the shortest direction to move.
Start moving the stepper.
Record the new position as the last position ready for the next move.

Error checking
===============

Error checking is pretty basic, and there's nothing stopping invalid values being programmed into the various CVs in use, however the validity of the CV values is checked prior to performing any actual stepper moves.

Any errors are printed to the serial port.

Decoder base address
=====================

The validity of the stored decoder base address (CVs 1 and 9) is checked on start up, and if invalid, the default accessory address of 1 is used instead.

Position definitions
=====================

The validity of the stored position definitions are checked both on startup, as well as every time an accessory packet is received to be acted upon.

If any part of a postion definition is invalid, it is effectively ignored in order to prevent attempting to move the stepper motor an invalid number of steps, or to attempt to send anything other than a 0 or 1 to the relay inputs.
