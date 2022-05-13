********************
Hardware components
********************

Arduino Uno
============

I'm using a generic Arduino Uno R3 to drive the turntable which is a Duinotech brand sourced locally here as part of a starter kit. There's no reason I can think of, however, that a Nano, Mega, or any others would work providing they provide sufficient digital inputs and outputs and have sufficient memory.

The code requires 2 digital inputs (one must be interrupt driven) and 7 digital outputs. Incidentally, the only reason I use A1 for the DCC ACK signal is because I blew the output of my Uno's pin 3.

At the time of writing, when compiled, the sketch uses 15986 bytes of program storage space, and global variables use 1023 bytes of dynamic memory.

ULN2003/28BYJ-48 stepper driver and motor
==========================================

The 28BYJ-48 is an inexpensive unipolar stepper motor used in many consumer devices and is an ideal candidate for a small scale turntable. The motor is driven by the ULN2003 driver using 4 pins as outputs from the Arduino in full step mode. The datasheet for the stepper indicates it takes 2048 steps for a full revolution in full step mode, or 4096 steps in half step mode.

While I haven't used the stepper in anger on a fully functioning layout yet, turning an N scale loco on my partially complete bridge deck works well, so I'm confident it will suit at least smaller scale layouts. My aim is to have the bridge deck on wheels running on the pit rail to support the weight, so the stepper will only have rotational forces to work against.

I simply stuck with the pin connections as defined in the datasheet for the specific ULN2003 I purchased, which uses pins 8 through 11.

The important thing to note when initiating the stepper motor object is that the pins aren't referred to linearly from 8 to 11, but rather have a specific order they need to be defined in. I've provided two alternatives in the code depending if you prefer the default direction to be clockwise or anti-clockwise.

Hall effect sensor
===================

Ready made Arduino compatible hall effect sensors are readily available (and cheap) and I simply connect one of these to pin 3, which sends the input LOW when activated. Note that some appear to have a HIGH active state instead, so the "#define HOME_SENSOR_ACTIVE_STATE LOW" line in the sketch will need to be adjusted to "#define HOME_SENSOR_ACTIVE_STATE HIGH" in order for these to work correctly.

Aside from the input pin, these simply require a 5V and ground connection.

Dual relay board
=================

I've chosen to use a dual relay board to control the polarity of the bridge deck track as it was simple enough to incorporate into the code with a simple polarity flag, and I don't have a short-circuit detection type auto reverser to perform that function.

Prototype shield
=================

The simplest and neatest way to be able to run a 5V regulator and the opto isolator circuit for the DCC decoder was to obtain an Uno footprint prototype shield. There is more than enough room for the components, and the Uno shield form factor means it's a neat fit.

Power supply/voltage regulator
===============================

All components in use require 5V DC to operate, and the recommendation for the stepper motor and driver combination is to use an external 5V supply as the current requirements may exceed what the built-in Uno 5V regulator can supply.

I had an LM7805, a 220nF polyester film, and 0.1uF ceramic capacitor on hand so chose to make my own voltage regulator circuit as the power supply for all components using the prototype shield.

My input voltage is 8.5V DC, which seems odd but turns out to have been the perfect voltage to drive my Rokuhan turnouts reliably while still staying below the recommended 9V DC maximum input for Arduinos.

DCC Decoder circuit
====================

This is where full credit goes to the team at https://mrrwa.org/ for making all the DCC decoder information for Arduinos readily accessible. There are three designs referred to on their DCC interface page: https://mrrwa.org/dcc-decoder-interface/

I made my own decoder circuit using Wolfgang Kuffer’s design on the prototype shield as I had most components already on hand except for the two optocoupler (which is dirt cheap). Note, I didn't bother with the ACK circuit as most of the programming will be in ops mode (program on main), and the ACK isn't required or functional as a result.

The DCC signal is connected to pin 2 on the Uno as it's an interrupt pin. Note that despite the ACK circuit not being used by me, the code is still present should you wish to use it.
