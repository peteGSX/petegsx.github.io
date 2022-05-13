*********
Overview
*********

A turntable was always going to be a central feature of my layout, and I specifically wanted one that was somewhat prototypical of what was (probably) in use at the time. I'm in Brisbane, Australia, and the local railroads here are narrow gauge, and therefore I needed a relatively small (60') turntable which will have Z track on the bridge deck.

Given my layout will be DCC controlled, obviously the turntable needs to be also, and I felt there was a need to have an easy way to update the various turntable positions with the turntable installed to make minor track alignment adjustments without having to connect to the programming circuit or having to plug in a serial cable, hence the desire for a turntable controller I could program "on the fly".

I happened to have an Arduino Uno R3 available along with some strip board, a voltage regulator, and a few other bits and pieces lying around, so making my own DCC decoder board was pretty straight forward with very few purchases, and the other components required were readily available locally.

The code has taken some time to get my head around and the core is essentially a modified version of the "DCCInterface_TurntableControl" example by Alex Shepherd included with the NmraDCC library, so much credit to Alex and all the others who have contributed to that library as this wouldn't be possible without it. Take note I am not a developer in any way shape or form, so there are likely inefficiencies and bugs hidden in there somewhere.

Credit also to the guys on the DCC++ EX Discord server for input into making the code better as well.
