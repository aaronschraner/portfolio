---
title: "Breadboard Nixie Tube Clock"
date: 2018-08-27T16:54:07-07:00
draft: true
---
![PCB pending](https://i.imgur.com/jWj98FP.jpg)

Description
-----------
This project is a digital clock that uses IN-14 nixie tubes to display the time. It is controlled by a raspberry pi using shift registers. I did this project in 2016 but didn't have any online documentation except for the [github repo](https://github.com/aaronschraner/nixie-clock) and a [youtube video](https://www.youtube.com/watch?v=dKM_yw2h1mo) until now. 

Schematic
---------
![Tube pair](https://i.imgur.com/c1SpQ4V.png)
![Top level](https://i.imgur.com/zrVtCN7.png)
[PDF version](/bbntc_schematic.pdf)

Software
--------
The software is relatively simple. The clock is controlled by 3 shift registers with separate data lines and the clock/latch lines tied together. It uses [wiringPi](http://wiringpi.com/) to interface with the pins. The software is in a [github repository](https://github.com/aaronschraner/nixie-clock)

Hardware
--------
The high voltage supply for the nixie tubes is an [NCH6100HV High-voltage DC-DC converter module](https://www.amazon.com/Westsell-NCH6100HV-Voltage-Supply-Module/dp/B07G9HVSX9/). This is powered by a 12V power supply I got from a friend. The device is controlled by a raspberry pi 2 model B.


