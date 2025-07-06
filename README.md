# T41-2 Low Power Amplifier Version 1.6

This is the PCB for the Low Power Amplifier for the T41 "Software Defined Transceiver".
This PCB was designed using the open-source design tool Kicad 9.0.

The Low Power Amplifier is designed to drive the T41-2 Power Amplifier, described here:

<>

The Low Power Amplifier combined with the Power Amplifier are intended to replace the
original V11 Power Amplifier which uses IRF510 switching MOSFETs in the final amplifier
stage.  This new design will improve all aspects of power amplifier performance, 
including linearity, power, efficiency, and bandwidth.  An important difference is that
the amplifier operates from a 13.8 volt supply.  No "boost" module is required.

The schematic is here:

<>

# Design Details

## First Amplifier Stage

As the T41 is an "Experimenter's Platform", the Low Power Amplifier includes circuits
which are intended to test ideas which could possibly be used in other applications.

The input includes a pi resistive attenuator.  The schematic shows fixed values, but
these can be altered to match a particular application.  The values shown are intended
to work with the output level of the QSE, which is about -10dBm.  Note that the second
shunt resistor is "DNP" (Do Not Place), as the input of the amplifier provides the
required shunt impedance.

The first stage, which is actually a two-stage amplifier, is a discrete implementation
of a "Darlington" style RF amplifier.  This is an experiment I have wanted to try for
quite a while.  Darlington RF amplifiers are available in numerous configurations
as integrated circuits, however, I wanted to see if a wideband Darlington could be
made to work with discrete NPN transistors.  After numerous experiments, it was
decided to use the BRF106 BJT device in the circuit.  The feedback values were adjusted
to achieve desired impedance and gain levels.

It did not appear to be a good idea to run the Darlington amplifier from the 13.8 volt
supply.  It is important to keep the voltages and currents stable, which in turn keeps
impedances and gains constant.  This means a voltage regulator had to be added to the
circuit.  A SOT-23-5 package 10 volt regulator was found which works perfectly.  This
regulator has the benefit of a shutdown pin.  The shutdown pin is connected to the
TXRX signal.

## Second Amplifier Stage

In order to drive the Power Amplifier, the second stage of the Low Power Amplifier
needs something on the order of a quarter to half watt output power with good
linearity.  Strangely enough, this is something which may be more difficult to
achieve than it was in the past.  At least with discrete components, which was a
primary goal of this design.

Back in the "good old days" there were devices like the 2N4427, 2N3866, and 2N5109
in the sturdy metal TO-5 package:

<https://en.wikipedia.org/wiki/TO-5>

Now I could probably find a cache of the old TO-5 parts, but what I wanted was the
"modern" version of these devices.  That turned out to be a difficult search!
This is what seemed to be the 21st century RF low-power device:

<https://www.nxp.com/part/BFU590G#/>

But even this device has a last-time buy date of June 2026!  Fortunately they
are still in stock at the usual distributors.  In quantities of 10, they cost
US$0.77, so quite a bargain for a 8.5GHz RF device.

After a bit of simulation, the chosen amplifier circuit is simple.  By using 
series and shunt feedback the amplifier has good linearity and power.

Next, putting the gain stage into a push-pull configuration was required to maximize
power and cancel even harmonics.  A simple class-AB bias circuit uses another RF
transistor, the BRF92, to stabilize the DC bias current.

A second 10 volt regulator is used to bias the output stage.  This regulator has output
current limiting (about 200mA) and thermal shutdown.  The SOT-89-5 package can dissipate
quite a lot of power, thanks to the large ground tab.

There is also an optional "thermostat" device which shuts down the amplifier if the
temperature rises above a threshold set by a resistor value.  The thermostat is
positioned in close proximity to the output amplifier devices.  Experiments are
ongoing with this device to determine what temperature setting should be used
and if it is even necessary at all.

# Build Instructions

# Tune Up

## DC Bias Adjustment

## Linearity Testing

