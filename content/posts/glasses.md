---
title: "High Brightness LED Glasses"
date: 2019-10-08T22:59:14-04:00
---

![](https://i.imgur.com/d11aYmN.jpg "The device")

Description
-----------
This project started as a last minute birthday present idea for a friend of mine who is also an electrical engineer.

The idea started in 2018 when I decided to prank him by waking him up with some high brightness LEDs I had recently bought:

![](https://i.imgur.com/j2Ch7Ei.jpg "The wake up call that started it all" )

The LEDs run at about 18 volts at 3A max so to power them I originally used my benchtop power supply

The goal with this project was to do something similar but make it portable.

Features
--------
* Wireless brightness control via nRF24L01 2.4GHz radio module
* Digitally controlled boost converter with variable duty cycle
* Digitally controlled low-side constant current LED driver circuit
* ATTiny84 AVR microcontroller
* Hardware output voltage runaway protection for boost converter
* Analog readback from low-side CC source for maximizing efficiency and minimizing waste heat
* Uses same low power remote as audio visualizer project. 
* Powered by 9V battery

Schematic
---------
(TODO: needs redraw in schematic capture software)
![](https://i.imgur.com/pf24917.jpg)

Theory of operation
-------------------
### Digital control
Both the switching power supply and constant current LED driver are controlled by hardware PWM with timer/counter 0 on the ATTiny84.

The `OC0A` pin is connected to the gate of the switching FET of the boost converter through a resistor, which is part of the runaway protection circuit. When triggered, this circuit grounds the gate and prevents the converter from switching.

The `OC0B` pin is connected to a combined voltage divider and RC low-pass filter, which is designed to take the 0-5V PWM signal and convert it to a smooth voltage between 0 and 200mV. When fed into the transconductance amplifier circuit, this is converted to a constant current sink from 0 to 2.2 amps, which is split between the two LEDs. The components are chosen to provide an optimal output range for the LEDs with a time constant that is large compared to the switching period of 32us. I chose a value of RC = approx 2ms.

### Remote
The remote sends a packet containing either the `+`, `-`, or `?` character to increase, decrease, or toggle the brightness respectively. I reused the remote and nRF24 driver code from a [previous project.](/posts/led-strip-audio-vis) 

The remote only draws about 2.4 microamps in standby. As of time of writing I still have not needed to replace the original batteries despite having it on for over a year.

### Boost converter and CC driver
I found in testing that the full range of current for the LEDs that the constant current driver could provide was much too bright and produced too much heat in the LEDs. In the current version of the software the constant current driver is fixed at 10% duty cycle which limits it to about 100mA per LED. The brightness is modulated by varying the duty cycle of the boost converter from 0 to 40%. 

This also worked out because while my bench power supply can supply up to 3 amps, the 9V batteries I've used can only manage about 800mA.

The LED brightness can be limited by either the constant current source or the boost converter output.

The approximate maximum current for the CC driver as a function of OCR0B is `I =  2.2A * OCR0B / 255` 

This current is split between the two LEDs which each receive half. The software fixes this at a maximum of about 430mA combined for the two LEDs.
The calculated max current output for the boost converter is `I = 3A * (OCR0A/255)^2`. The software defined maximum of 100 equates to about 460 mA. 

### Runaway protection and feedback
   In the event that the LED current limit is set too low and the boost converter duty cycle is too high, the output voltage will rise until the cathode of the LEDs reach about 2V, at which point a BJT grounds the gate of the switching MOSFET, preventing it from dumping more current into the output capacitor and damaging the constant current sink FET. 
   An LED is wired inline with the base of the BJT to give a visual indication of if this feature is active.
   
   A 4.7k resistor is wired in parallel with the LEDs on the circuit board to protect the FET in the event one of the LED wires breaks.
   
   The cathode of the LEDs is also fed to an analog input to enable the MCU to detect if the runaway protection circuit is triggered, though this is not yet implemented in the software.
   
   More details on the implementation of the remote are available on my [audio visualizer project post](/posts/LED-strip-audio-vis)

### Software
   The code for this project is posted at https://github.com/aaronschraner/glasses

   It is written in C++ and compiled with `avr-gcc` (see Makefile)

   Toward the end of the circuit construction I ran out of space for the nRF24 module. Since it uses many of the same SPI pins as the AVRISP programming interface, I decided to put it on a detachable breakout board (yellow) that slots over the programming header. 


Does it work?
-------------

### Yes.
![](https://i.imgur.com/zndSrtm.jpg)




