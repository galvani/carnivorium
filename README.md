# carnivorium
My Carnivores


## Tech

### Here's how to figure out what resistor you need. First, a few things we know:

* The Darlington has two base-emitter junctions in series, so the turn-on voltage is about 1.4 volts (that is, the usual 0.7 times 2).
* The data sheet says the current gain MINIMUM is 1000
* The Arduino output pin should be limited to about 10 milliamps so that when other pins are also used, we don't exceed the specs of the AVR chip.
* For PWM motor speed control, we are not working in the linear region. We want the transistor to "slam" on and off as solidly as possible.
* The Arduino pin output voltage is 5 volts.

OK, now a few calculations:

* The voltage drop across the resistor is V/R. We don't know R yet, but we do know V... it's 5 - 1.4 = 3.6 volts.
* We want to put no more than 10 milliamps load on the PWM pin, so our I is defined... 0.01 amps.
* Georg Ohm says that R = V / I.... therefore R = 3.6 / 0.01 = 360 ohms which we can slide up or down to standard values (i.e. 330 or 470). Let's pick 330... that makes the pin current 10.9 milliamps... no big deal.

Now, are we giving the transistor enough drive? Let's see... 10.9 milliamps * minimum current gain of 1000 equals 10.9 amperes!  Since the fan probably draws an amp or two at most, we are certainly WAY well into saturation of the collector.

Lastly, the TIP-120 has a built in snubber diode, so you don't even need an external diode.

In summary: Transistor: TIP-120. Base resistor: 330 ohms. You're good to go!
