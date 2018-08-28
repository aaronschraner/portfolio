---
title: "Breadboard Nixie Tube Clock"
date: 2018-08-27T16:54:07-07:00
---
![PCB pending](https://i.imgur.com/jWj98FP.jpg)

Description
-----------
This project is a digital clock that uses IN-14 nixie tubes to display the time. It is controlled by a raspberry pi using shift registers. I did this project in 2016 but didn't have any online documentation except for the [github repo](https://github.com/aaronschraner/nixie-clock) and a [youtube video](https://www.youtube.com/watch?v=dKM_yw2h1mo) until now. One of the key features of this project is that since it is powered by a raspberry pi, it can be easily controlled from within python or bash scripts, and is automatically network synchronized as long as the pi has an internet connection. Before shelling out the $28 for a high voltage DC-DC converter, I used a (free) disposable camera flash circuit, which had to be submerged in mineral oil for cooling because it was being driven at several times its intended power output. 

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
The high voltage supply for the nixie tubes is an [NCH6100HV High-voltage DC-DC converter module](https://www.amazon.com/Westsell-NCH6100HV-Voltage-Supply-Module/dp/B07G9HVSX9/). 
This is powered by a 12V power supply I got from a friend. 
The device is controlled by a raspberry pi 2 model B, but any model of raspberry pi should work. 
The components used include: 

 * [12x ULQ2004a darlington BJT array](https://www.digikey.com/product-detail/en/stmicroelectronics/ULQ2004A/497-2360-5-ND/599623)
 * [6x CD4028be 4-to-10 BCD decoder](https://www.digikey.com/product-detail/en/texas-instruments/CD4028BE/296-2045-5-ND/67273)
 * [3x SN74HC595N 8-bit serial-in-parallel-out shift register](https://www.digikey.com/product-detail/en/texas-instruments/SN74HC595N/296-1600-5-ND/277246)
 * [6x 10k 1/4W resistors](https://www.digikey.com/product-detail/en/stackpole-electronics-inc/CF14JT10K0/CF14JT10K0CT-ND/1830374)
 * [3x full-size breadboards](https://www.digikey.com/product-detail/en/twin-industries/TW-E40-1020/438-1045-ND/643111)
 * Assorted lengths of wire, including some to connect to raspberry pi header pins.


