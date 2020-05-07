# SCOPETREX
## Vector Gaming on Your Oscilloscope!

Have you ever wanted to buy a Vectrex, but you can't afford the high prices on
auction sites? Do you already have a hoard of Vectrexes, but want *another*
one? Well now you can build your own!

![SCOPETREX photo](https://github.com/schlae/scopetrex/blob/master/images/scopetrex.png)

The SCOPETREX is basically a Vectrex on a single board without a monitor.
To play games, you have to connect it to an oscilloscope or an XY monitor.

This board is not just an exact clone of a Vectrex; it makes a number of
improvements over the original.

* Single +5V power supply, only 500mA (minimum)
* Configurable X and Y size and polarity
* Configurable brightness and video blanking polarity
* Works with a 68A09/68B09 or the more common 68A09E/68B09E
* Works with the AY-3-8912 sound chip or the cheaper AY-3-8910/YM2149F
* Custom controller board which is also compatible with the Vectrex
* Cool art on the board

All of the components are readily available, either from Mouser or from
various brokers in China. The bills of materials include Mouser part numbers.

[Here is the schematic](https://github.com/schlae/scopetrex/blob/master/Scopetrex.pdf).

There are two separate bills of materials. One is configured for people who
wish to build their SCOPETREX with the 68A09/68B09 (no suffix option), and
the other is configured for the 68A09E/68B09E (note the **E** suffix). In
general, the **E** suffix is easier to find and it is less likely to be a
counterfeit part. One caution: the 6809 and 6809E (no A or B) chips are only
rated to 1MHz while the SCOPETREX requires 1.5MHz operation.

[Bill of Materials, 6809 (plain) version](https://github.com/schlae/scopetrex/blob/master/Scopetrex_6809.csv)

[Bill of Materials, 6809E version](https://github.com/schlae/scopetrex/blob/master/Scopetrex_6809E.csv)

Please note that the 0.1" header pins are *not* listed on the BOM. They are
just standard breakaway headers. Jumper shunts (you will need three) are also
not listed on the BOM.

The game cartridge slot is designed to be used with the Sullins EBC18DRAS
(listed in the BOM as S3311-ND) but you can also use the EDAC 395-036-520-202
since it is available from Mouser and it may be more convenient to order all
the parts at once. If you do this, you will need to install the EDAC slot
at a right angle and add 18 bodge wires (see the Assembly Notes section).

[Here are the fab files](https://github.com/schlae/scopetrex/blob/master/fab/Scopetrex.zip).

Board dimensions are 7 x 5 inches. Order the board in whatever cool colors
you like!

## The Controller
The SCOPETREX also has a controller.

[Schematic](https://github.com/schlae/scopetrex/blob/master/controller/controller.pdf)

[Bill of Materials](https://github.com/schlae/scopetrex/blob/master/controller/controller.csv)

[Fab files](https://github.com/schlae/scopetrex/blob/master/controller/fab/controller.zip)

The board is 5.8 x 2 inches. It's very simple, so before fabbing it out,
considering going into Kicad and customizing it to your tastes. Add some fancy
silkscreen artwork or whatever you want.

The thumb joystick is listed with a Digi-Key part number since Mouser doesn't
carry it, but you can also get it from [Sparkfun](https://www.sparkfun.com/products/9032). There are similar joysticks sold by a number of different vendors
but this is the only one that's been tested.

There is a slide switch with 4 positions that selects which button (1 through
4) the top hat control triggers (when you push down on the joystick).

## Firmware
The SCOPETREX will run with the standard Vectrex firmware. Just program it
into the flash memory chip (the AT28C64). Note that the "Vectrex BIOS" ROM that
you may find does not include the MINE STORM game. Often, the "MINE STORM" ROM
comes with the BIOS so you should use that instead. I will not tell you where
to get ROMs, nor will I send you any. You could go buy a broken Vectrex and
transplant the ROM from that.

## Assembly Notes

In general it is a good idea to socket the chips that are hard to find and
thus may be counterfeit. It makes troubleshooting much easier. Therefore,
consider socketing the 6809, the 65C22, and the AY-3-8910/12.

The U101/MC34063 power supply chip should be soldered directly to the board
for best performance since a socket adds resistance.

The game cartridge connector has two different part numbers on the BOM. If
you ordered the EDAC part from Mouser which is designed to mount vertically
on the board, you will not be able to plug the cart into it because the case
will bump into components on the board. I recommend rotating the connector
90 degrees and soldering the bottom 18 pins directly to the footprint and
connecting the top 18 pins using bodge wires.

![Photo of EDAC connector bodge](https://github.com/schlae/scopetrex/blob/master/images/edac_bodge.png)

Don't forget to install the jumpers J301, J302, and J303. If you aren't sure
what polarity you need, just set them all to "NORM."

Set all the trimmer potentiometers to the halfway position. You'll tune them
later on.

Don't forget to flash the firmware into the AT28C64. There are many devices
that can do this. I like the MINIPRO programmers that are available cheaply
from many different sources.

When you assemble the controller board, be sure to install the DE-9 connector
on the bottom of the circuit board rather than the top.

## Initial Powerup and Calibration
You can connect your oscilloscope probes to the X, Y, and Z (aka blanking)
directly or by making up adapter BNC cables that go directly into your
oscilloscope or XY monitor inputs.

To start with, connect just the X and Y outputs to your oscilloscope's channel
1 and channel 2 inputs. Set both channels to 1V/div and put the oscilloscope
into XY mode (on some oscilloscopes, you do this by rotating the horizontal
sweep rate knob all the way counterclockwise).

**Be very careful about setting the brightness/intensity control on your
oscilloscope. A spot that is too bright can permanently damage the phosphor
coating inside the CRT, leaving a dark spot!**

Connect a 5V power source to the input jack on the SCOPETREX and move the
power switch to the ON position. After a second you should see lines and dots
appear in various places on the oscilloscope. You may have to adjust the
intensity knob to be able to see them.

Next, connect the oscilloscope's Z axis input (sometimes called video or
blanking) to the Z axis output of the SCOPETREX. Try adjusting the brightness
trimmer on the SCOPETREX. If you still see a lot of lines and a bright spot
in the middle of the screen, switch the polarity jumper on the Z axis (JP301).
Adjust the brightness trimmer again until the spot in the center goes away.

At this point you can also plug in a controller and some speakers into the
audio jack. Make sure you can get sound, and check if the controller works.

The SCOPETREX requires some calibration to be performed to get the best image
quality. To do this, you will need a Vectrex test cart (often included in
multicarts, which you probably want to have anyway.)

The first step of calibration involves correcting the DAC offset voltage. With
the test cart installed (no hot swapping carts! label side up!) you will first
see a grid displayed on the screen. Hit button 4, and the display should read
"DAC OFFSET," slowly blinking on and off. Connect a voltmeter between ground
(I like the convenient mounting holes in the corners of the board) and the left
side of R303 (marked with an arrow on the board). This is the voltage output,
pin 1, of the U304 op amp. With the text *off*, the voltmeter should read 0V.
If not, adjust the DAC offset trimmer until you get the voltage to 0V.

The second step involves fixing the X and Y adjustments. You can do this with
the test cart's third screen by pressing button 4 again. You'll see some
diamond-shaped targets; adjust X and Y so that the vertical and horizontal
lines are center inside the diamond shapes.

The third step is less specific, try hitting buttons 3 and 4 to switch to
various screens. Adjust the X and Y as you like to get things to look good.

The final step is the joystick calibration. Go to the last screen--the one
that you can't seem to exit by pushing a button--and adjust the two trimmers
on the *controller board* until the line segment turns into a dot. Swirl the
joystick around to make sure it hits all the square boxes. To exit this screen,
you have to push buttons 1 and 3 or buttons 1 and 4 at the same time.

## XY Monitors

XY monitors such as the Tektronix 602 or 604 offer a nicer experience for
playing Vectrex games. Typically they have a fixed analog deflection voltage of
only a volt or two, so you will need to use the width and height trimmers to
dial back the deflection so that all the objects are on the screen.

Pro tip--turn a landscape-mode XY monitor up on its side and swap the X and Y
inputs to mimic the Vectrex's portrait orientation.

## Troubleshooting
The SCOPETREX is a fairly complex mixed-signal board. I can't tell you all the
possible ways it can go wrong, but here's a list of things to check...
* Power supply voltages: Are +5V, -5V, and the -12V rails all present?
* Reset signal: Does the reset input on the 6809 go high?
* Does the 6809 have a valid set of clock signals? Check E and Q, and the
crystal or oscillator
* Is there activity on the bus? Check the address and data lines
* Does the ROM chip ever get selected? Both the CS# and OE# lines must be
pulsing for that to happen. How about the RAM chip?
* Check for activity on the 65C22 outputs
* Does sound come out of the AY-3-8910/2?
* Look at the waveform on pin 1 of U304A. You should see a fairly complex
waveform
* The SCOPETREX works by using a constant voltage into an integrator to
generate ramps that drive the X and Y deflection signals. Work your way back
along the analog signal chain starting from the individual deflection outputs
* Take a look at the blanking signal (Z axis) output magnitudes. You might
want to check the manual for your oscilloscope to find out the acceptable range
of voltages

## Other Notes

After all that work, don't forget to enjoy playing some Vectrex games!

## License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0
International License. See [https://creativecommons.org/licenses/by-sa/4.0/](https://creativecommons.org/licenses/by-sa/4.0/).


