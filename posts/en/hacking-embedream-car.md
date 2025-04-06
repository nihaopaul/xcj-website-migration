---
id: 980
title: Hacking Embedream Car
date: 2011-05-06 03:43:00
author: 5
---

Today I saw an embedded dream car, but after turning it on, it ran wildly, so I reprogrammed it. However, there was no network in the new workshop, so I tried it step by step. The results are as follows:

CT1 receives PWM and controls speed.
CT2 is the forward control signal, and a high voltage activates the motor.
CT3 is the reverse control signal, and a high voltage activates the motor.

However, there was a problem with the connection between the UNO on the car and my Ubuntu. It seems that only Windows works well, while Mac OS sometimes has problems. Therefore, a Mega 1280 was used on the car in the end.

However, another problem was discovered: when the Arduino is powered by USB, everything is normal, but when the car's built-in 5V power supply is used, the program becomes erratic and completely random. It is speculated that the motor rotation causes a voltage drop in the entire system, which cannot provide enough voltage to the Arduino board. This might also be the reason why the UNO did not run erratically before. Therefore, a 9V layered battery was added to the car to power the Arduino. Finally, it worked.

The program's function is to move forward, reverse, turn, and continue moving forward when an object is detected in front, creating a simple obstacle avoidance program. Speed control was not used.

The following is the final appearance of the car. Taken with a phone, so the quality is not ideal.

Left side photo
Right side photo
Another photo
Another photo

The program used is below: