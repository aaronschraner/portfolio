---
title: "Multimeter Watch"
date: 2018-08-30T17:48:56-07:00
---

![Measuring voltage](https://i.imgur.com/ENSOZiT.jpg)
![Measuring resistance](https://i.imgur.com/undefined.jpg)
![Built-in flashlight](https://i.imgur.com/biotC4o.jpg)

Description
-----------
This project is a small form-factor digital multimeter capable of measuring DC voltage (up to +/-60V) and resistance. It is powered by an [ADS1115 ADC module](https://www.adafruit.com/product/1085) and ATMega328P microcontroller. The screen is a Broadcom HCMS-2912 dot matrix display, which has integrated brightness control and refresh circuitry. I built it in Spring 2017.

Features
--------
The multimeter is capable of measuring DC voltage up to +/- 60 Volts and resistance from 100 ohms to 50 kohms. It also has a built-in flashlight.

Backstory
---------
In week 7 of Spring 2017, I got an email from the OSU scholarship office saying that because I had failed a class in winter term, I was not on track to meet the credit requirement for my scholarship by the end of the year. 
I visited the scholarship office that day and asked them what my options were, and they told me that there was nothing I could do except apply for a different scholarship and hope for the best. This really wasn't a good option for me, so I met with an advisor in the college of EECS (Nick Malos), who told me my options were limited, but not nonexistant. He suggested I do a project for the 2 credits I needed to keep my scholarship another year. I asked Don Heer to sponsor the project (approve the proposal and check that I met the requirements at the end of the term) and he agreed. At this point it was almost the end of the term, and I had to finish the project in addition to studying for finals and wrapping up other classes.
I finished the project around 5 AM on June 16th, the day of my final checkoff with Don and my 19th birthday. Though the resistance measurement functionality was on the edge of being out of spec, Don approved the project and I was able to keep my scholarship for my final year at OSU. 

Issues
------
I originally had plans for the multimeter watch to work like a normal watch - with the ability to display the current time, but I think I made an error in calculating the capacitor values for the 32kHz crystal circuit, because instead of acting as a 32kHz oscillator, it acted as a high voltage detector which rapidly incremented timer/counter 2 whenever the circuit was near high voltage AC sources. 

As mentioned in the backstory for this project, resistance measurement is also a bit of an issue. The resistor in the picture at the top of the page is 2.2kohms with 5% tolerance, but because the resistive voltage divider circuit is powered directly from the batteries and the ADC has an internal reference, the resistance measurement circuit is highly sensitive to how fully charged the batteries are. 

You might also notice multiple unpopulated IC sockets and large resistor array on the left of the board. These are evidence of my original plan to include some [small red HP bubble displays](https://www.sparkfun.com/products/retired/12710) in addition to the HCMS display, but unfortunately I ran out of time and wiring space before finishing this part of the board. 

Unfortunately I wasn't very careful about documenting the design of this project, or keeping the software in an easy to find place. I still haven't found a working version of it on my computer, or any of the schematics I drew on paper.

Non-issues
----------

The voltage measurement functionality is definitely the highlight of this project. Because the ADS1115 has a highly accurate internal voltage reference, and because I calibrated it using my Fluke 87V multimeter, voltage is accurate to +/- 2 least significant digits on the display, or about +/-20mV. 

I haven't found the software or schematics yet, but I do remember that it averages several readings from the ADS1115 and feeds it into a linear function that converts the ADC value into a voltage, which is displayed on the screen. The meter is calibrated by adjusting the values in the linear conversion function. 

This could be called a feature or a drawback, but I'm going to call it a feature. The meter has separate pins for voltage measurement and resistance measurement. This makes it easy to quickly toggle between probing a circuit with the two voltage leads and sticking a resistor in the two holes that are spaced to easily accomodate a resistor. 


