************
Programming
************

The turntable will require programming of both the base decoder address to respond to as well as the turntable positions.

Base decoder address
=====================

The base decoder address is made up of the 6 least significant bits in CV 1 (cvLSB), and the 3 least significant bits in CV 9 (cvMSB).

I happen to run my turntable with a base address of 201, which requires CV 1 to be set to 51 and CV 9 to be set to 0.

The formula to calculate this is: (((cvMSB * 64) + cvLSB - 1) * 4) + 1

In my case, this translates to: (((0 * 64) + 51 - 1) * 4) + 1 = 201

This formula originates from having a DCC accessory board being capable of driving four outputs.

Turntable positions
====================

The turntable positions are defined in the manufacturer reserved CVs starting at 513 as per the NMRA standard.

CV 513 contains the number of positions being defined, with a valid maximum of 50 positions available.

Each position definition requires three CVs to be programmed starting at CV 514:

The least significant bits (LSB) of the steps to be moved for the defined position.
The most significant bits (MSB) of the steps to be moved for the defined position.
The polarity flag for the defined position (0 for retain existing, 1 to reverse polarity).
The code performs an 8 bit left shift on the MSB before adding the LSB to determine the number of steps for the position.

This is an example table for a six position turntable definition:

+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| Position | DCC Address | Steps from Home | LSB CV | Value | MSB CV | Value | Polarity CV | Value |
+==========+=============+=================+========+=======+========+=======+=============+=======+
| 1        | 201         | 12              | 514    | 12    | 515    | 0     | 516         | 0     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| 2        | 202         | 42              | 517    | 42    | 518    | 0     | 519         | 0     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| 3        | 203         | 126             | 520    | 126   | 521    | 0     | 522         | 0     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| 4        | 204         | 210             | 523    | 210   | 524    | 0     | 525         | 0     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| 5        | 205         | 1122            | 526    | 98    | 527    | 4     | 528         | 1     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+
| 6        | 206         | 1164            | 529    | 140   | 530    | 4     | 531         | 1     |
+----------+-------------+-----------------+--------+-------+--------+-------+-------------+-------+

Service mode programming
=========================

The typical way of programming decoders is to connect them to a programming track which allows for service mode programming.

The NmraDcc library enables this functionality, so programming in service mode is as straight forward as connecting to the programming track and performing the programming activities.

I use the JMRI single CV programmer for these activities.

I'd recommend using service mode programming to set both the decoder base address and the ops mode address. Defining the turntable positions can be done in either service mode or ops mode once these are set.

Ops mode programming (Program on Main/POM)
===========================================

I found it important to incorporate the ability to perform ops mode programming once the turntable is permanently in place to have a simple method of making adjustments to the defined positions in order to get track alignment for each position as accurate as possible and to allow for any variations once the home sensor is mounted permanently.

In order to enable ops mode programming, the DCC library needs to have a CV provided that contains the DCC decoder address to respond to for programming commands.

To facilitate this, the manufacturer reserved CV 112 is used to contain the DCC decoder address, and I simply program CV 112 with the same address as the base address for the turntable (201 in my case).
