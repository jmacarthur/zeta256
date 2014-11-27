zeta256
=======

![Zeta Prototype](/images/zeta-web.jpeg)

The Zeta is a minimal Z80 toggle-switch computer. It has a Zilog Z80 microprocessor, 256 bytes of RAM and the only interface is the front panel which directly sets and reads the address and data buses.

There is a video of it executing Euclid's algorithm:

https://www.youtube.com/watch?v=0GmY_UrbXnA

## Overview

![Zeta Overview diagram](/images/overview.png)

At the moment, there is only one real source file in this repository, an Inkscape-produced SVG which contains the stripboard layout and lasercut paths along with the image for the box top. In the future I'll try to add a KiCad circuit diagram. This file doesn't preview well in github because there are some very thin and zero-width lines - turn on outline mode (View -> Display mode -> Outline) in Inkscape to view it.

Note that this isn't a foolproof guide to building a replica - there are several parts not recorded yet, such as where to cut the track on the stripboard, and some extra components for the voltage regulators.

There are some errata in the current source - please see the issues section for details.

## Why is your circuit diagram in SVG?

Because of the number of DIP chips in this project, it suits stripboard well, and I haven't found a good program for designing stripboard layouts yet. Fritzing supports small stripboard, but has performance problems when you use a layout as big as this one.

## How does it work?

The Z80 has two pins called !BUSREQ and !BUSACK. !BUSREQ is an input, normally high (5V), which means the Z80 is in control of the address and data buses, except when RD is high which means the RAM chip can control the data bus. The "Front Panel/Processor" switch on the front panel pulls !BUSREQ to 0V when "Front Panel" is selected. After a few clock cycles, the Z80 will then drop the output !BUSACK. This is connected to the output enable pins of the two input buffers (the SN74LVC245AN chips). The switch positions are then driven onto the buses, and you can enter data into the RAM using the write button.

The inverting schmitt trigger IC (74HCT14) performs debouncing for the clock line, and inverts and debounces the reset button. None of the other inputs are debounced.

The rotary switch is a 10 or 16 position encoded switch with the '1' line connected to the clock line and the common connector to 5V. Note that if you leave the rotary switch in an 'odd' position, the front panel clock button will not do anything.


