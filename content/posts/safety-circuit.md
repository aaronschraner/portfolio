---
title: "Safety Circuit"
date: 2018-08-30T19:40:29-07:00
---

![The most colorful board in senior design](https://i.imgur.com/6mrtbJ1.jpg)

Description
-----------
This circuit was a part of my senior design project, an electronic throttle for the OSU formula racing team. As part of the very long list of safety requirements an electronic throttle has to meet in order to participate in formula racing, there has to be a non-programmable safety circuit that is capable of cutting power to the engine if the throttle is open by more than 10% and the driver is braking hard for more than one second. 

Design
------
![Final schematic](https://i.imgur.com/ASQiPF0.png)
Note - this was a team project. This schematic was made by my teammate Mohammed Aljeelani, who created the PCB layout for the board. I came up with the original design but did it in a tool that was incompatible with EAGLE. That version of the design also does not have the hysteresis resistors, part numbers, or decoupling capacitors.

As part of the rest of the project, we already have access to two analog signals that represent the two throttle position sensors (TPS). These signals are fed into the safety circuit in addition to another signal from the brake, which outputs either 1.7 volts when not actuated or 2.5 volts when actuated (these strange voltages are for fault detection). 

The design can be broken up into 3 sections.

The first section, with the comparators and digital logic gates, detects the condition that should cause the circuit to trigger.
The way this section should operate is follows:

`output = !( ( (TPS1 > threshold) or (TPS2 > threshold) ) and (BRAKE > threshold))`

The first section of the circuit was designed by translating this statement into digital logic (AND and OR) gates and comparators with slight hysteresis to prevent oscillating behavior. 

The second section is the time delay stage. When the input to this stage is 0 volts, it causes the P-channel MOSFET to conduct and charge the capacitor to 5 volts. When the input is 5 volts, it causes a fixed current (set by a current mirror circuit) to flow out of the capacitor at a constant rate, until the capacitor voltage falls below a threshold set by potentiometer. Adjusting this pot allows you to change the delay to anything from instantaneous to about 2 seconds. 

The third and final stage takes the output from this comparator and, when it is true, triggers a relay circuit which disables power to the engine control unit and locks in the off position until power is disconnected from the car via the master control switch.

This was part of the Electronic Throttle Control system project in OSU ECE Senior Design 2017-2018. 
My teammates who worked with me on the project are Mohammed Aljeelani and Samantha Holman.

Last-minute problem solving
---------------------------
The custom mounting of the NOR gate IC pictured in the top image was our last-minute solution to a problem that took us all of Spring term to figure out. It turned out that we had accidentally ordered the wrong quad-NOR gate IC, which had an identical pinout to the one the PCB was based on, but with two of the pins switched. We used this small section of ribbon cable to switch those pins back and pass our final checkoff. 



[Link to google site](https://sites.google.com/a/oregonstate.edu/ece44x201709/ece-senior-design-example-project/documentation)



