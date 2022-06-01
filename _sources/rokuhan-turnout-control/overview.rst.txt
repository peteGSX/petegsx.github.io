*********
Overview
*********

`This repository <https://github.com/peteGSX-Projects/rokuhan-dcc-point-control>`_ contains the code for an Arduino based controller capable of switching either two or four Rokuhan brand electronic turnouts using DCC for digital control.

This uses either two L293D motor controller ICs or an L298 based motor shield to control the turnouts.

The code complies with the NMRA standard setting direction 1 for Closed, and 0 for Thrown.

*************
Instructions
*************

Rokuhan turnouts require a very brief pulse to switch the direction only, and continuous current will burn the motor out. This code has been written to cater for this.

I have found an input voltage of 8.5V to be reliable, meaning the same power source can be used to power both the Arduino itself as well as providing the switching voltage to the turnouts.

Digital Command Control (DCC) is used to trigger the turnout changes by inverting the direction, then setting the speed to max momentarily to trigger the change in direction.

*************
Arduino pins
*************

The code uses the pins below for the various functions:

DCC pins
=========

* D2 - Interrupt pin used for DCC decoding
* D3 - Used for the DCC ACK signal

Turnout 1 pins - connect to first L293D
========================================

* A4 - L293D input 1 - HIGH for through, LOW for branch
* A5 - L293D input 2 - LOW for through, HIGH for branch
* D5 - L293D enable 1 - set to max speed PWM 255 for 25ms to switch

Point 2 pins - connect to first L293D
======================================

* D4 - L293D input 3 - HIGH for through, LOW for branch
* D7 - L293D input 4 - LOW for through, HIGH for branch
* D6 - L293D enable 2 - set to max speed PWM 255 for 25ms to switch

Point 3 pins - connect to second L293D
=======================================

* D8 - L293D input 1 - HIGH for through, LOW for branch
* D11 - L293D input 2 - LOW for through, HIGH for branch
* D9 - L293D enable 1 - set to max speed PWM 255 for 25ms to switch

Point 4 pins - connect to second L293D
=======================================

* D12 - L293D input 3 - HIGH for through, LOW for branch
* D13 - L293D input 4 - LOW for through, HIGH for branch
* D10 - L293D enable 2 - set to max speed PWM 255 for 25ms to switch
