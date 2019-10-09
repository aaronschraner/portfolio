---
title: "High Brightness LED Glasses"
date: 2019-10-08T22:59:14-04:00
draft: true
---

picture of glasses in action
picture of electronics

Description
-----------
This project started as a last minute birthday present idea for a friend of mine who is also an electrical engineer
The idea started in 2018 when I decided to prank him by waking him up with some high brightness LEDs I had recently bought:

(photo of original power supply glasses)

The LEDs run at about 18 volts so to power them I originally used my benchtop power supply
The goal with this project was to do something similar but make it portable.

Features
--------
The glasses are powered by a 9V battery and feature:
- Wireless brightness control via nRF24L01 2.4GHz radio module
- Digitally controlled boost converter with variable duty cycle
- Digitally controlled low-side constant current LED driver circuit
- ATTiny84 AVR microcontroller
- Hardware output voltage runaway protection for boost converter
- Analog readback from low-side CC source for maximizing efficiency and minimizing waste heat
- Uses same low power remote as audio visualizer project. As of time of writing I still have not needed to replace the original batteries despite having it on in standby for over a year 

Schematic
---------
schematic goes here

Theory of operation
-------------------
Both the switching power supply and constant current LED driver are controlled by hardware PWM with timer/counter 0 on the ATTiny84.
# Remote
The remote sends a packet containing either the `+`, `-`, or `?` character to increase, decrease, or toggle the brightness respectively. I reused the remote and nRF24 driver code from a previous project.

# Boost converter and CC driver
I found in testing that the full range of current for the LEDs that the constant current driver could provide was much too bright and produced too much heat in the LEDs. In the current version of the software the constant current driver is fixed at 10% duty cycle which limits it to about 200mA per LED. The brightness is modulated by varying the duty cycle of the boost converter from 0 to 40%. 

The LED brightness can be limited by either the constant current source or the boost converter output.
The approximate maximum current for the CC driver as a function of OCR0B is `I =  4.4A * OCR0B / 255` - This current is split between the two LEDs which each receive half. The software fixes this at a maximum of about 430mA combined for the two LEDs.
The calculated max current output for the boost converter is `I = 1.5A * (OCR0A/255)^2`. The software defined maximum of 100 equates to about 230 mA. 

In the event that the LED current limit is set to 0 and the boost converter duty cycle is too high, the output voltage will rise until the cathode of the LEDs reach about 2V, at which point a BJT grounds the gate of the switching MOSFET, preventing it from dumping more current into the output capacitor and damaging the constant current sink FET. 
An LED is wired inline with the base of the BJT to give a visual indication of if this feature is active.

A 4.7k resistor is wired in parallel with the LEDs on the circuit board to protect the FET in the event one of the LED wires breaks.

The cathode of the LEDs is also fed to an analog input to enable the MCU to detect if the runaway protection circuit is triggered.

More details on the implementation of the remote are available on my audio visualizer project post


