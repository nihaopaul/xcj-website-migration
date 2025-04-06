---
id: 350
title: TX-2/RX-2: Heart of the cheap RC Toys from China
date: 2011-01-09 19:13:31
author: 2
---

To get ready for the Robot Contest event on 1/16, I ordered the RMB 58 RC cars from Taobao. This RC car is good size and properly built. Originally, I wanted to go with the route of replacing the control board with Arduino and drive everything there. As I was trying to hook up the motor to Arduino, I realized that there wasn't any H Bridge and it was way too cold to go out and get it. Hmm... I figure there must be some H Bridge on the control board I just ripped out of the car. As I located the two H bridge on the board, I noticed the RX-2 chip. Out of curiosity, I decided to google for this chip. To a pleasant surprise, I found RX-2/TX-2 Datasheet in Chinese and a guide for exactly the board in the car and remote. Decide to replace RX-2 in the car with Arduino so the H-Bridge on the board can be reused and the RF for the remote can still work. Still trying to figure out what I am going to do with those remote control signal. A few facts about RX-2/TX-2 chip I found is that the RC frequency can be adjusted by different resistance from 100K to 500K Ohm between OSCI/OSCO pins.