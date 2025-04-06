---
id: 177
title: A.R.T., PWM and RF
date: 2010-12-20 01:39:27
author: 4
---
## error
Failed to parse. Text: "```json
{"en": "A.R.T.: Autonomous Robot Toy ^\_^ Some theory gleaned related to PWM and RF. _Disclaimer: this is my first contact with PWM and RF... Feel free to correct me._ **General PWM introduction** Using the Arduino to drive the transmitter circuit would be a temporary hack. Best would be a simple circuit using a few dedicated ICs to achieve the same (specifically the [TX2C](http://www.datasheetarchive.com/pdf-datasheets/Datasheets-23/DSA-446609.html)). **Generating correct Pulse Modulation** I'm trying to get the Arduino to output a PWM that will drive the transmitter (using a crystal oscillator at a specific frequency) on/off to achieve the needed pulses.  According to \"[How Stuff Works](http://electronics.howstuffworks.com/rc-toy2.htm)\", RC control uses four pulses, each 2.1ms long, with 700µs intervals. The pulse segment (telling the antenna the new information) uses 700µs pulses with 700µs intervals. The number of pulses dictates the action: * Forward: 16 pulses * Reverse: 40 pulses * Forward/Left: 28 pulses * Forward/Right: 34 pulses * Reverse/Left: 52 pulses * Reverse/Right: 46 pulses Also: * RC control is 2.1ms HIGH + 0.7ms LOW (2.8ms total). * This is a 75% duty cycle and ~3571Hz frequency. * The pulse segment has a 50% duty cycle (pulse = interval) and a 714Hz frequency.  Using the [Arduino PWM tutorial](http://www.arduino.cc/en/Tutorial/PWM) we can specify the duty cycle and duration, but need a way to control frequency.  The Arduino (specifically the ATmega168) has a 16MHz clock with prescalers (1, 8, 64, 256, or 1024) that divide this to a timer.  Precise control is via an integer in the ICR. The microcontroller counts up to ICR then down to 0, going HIGH each time it reaches zero.  The equation is: desired_frequency = system_clock / (2 * prescaler * ICR).  For the 2.8ms pulse: * 16MHz / (2 * prescaler * ICR) =  3571 Hz  Solving for ICR (using different prescalers): * 1: ICR = 2240 * 8: ICR = 280 * 64: ICR = 35  etc.  For the 1.4ms pulse segment: * 16MHz / (2 * prescaler * ICR) = 714 Hz. Calculating similar ICR values for various prescalers.  Higher prescalers are generally better for lower power consumption.  The [ATmega timers tutorial](http://www.et06.dk/atmega_timers/) might help, but I don't fully understand it yet. **How to code this in Arduino?**  I'm unsure.  I've tried manually creating PWM with delays, but it doesn't work.  Buying the dedicated IC and using the provided schematics is likely easier.", "zh": "A.R.T.：自動機器人玩具 ^\_^  收集了一些關於 PWM 和 RF 的理論。_免責聲明：這是我第一次接觸 PWM 和 RF，請隨時更正我。_ **一般 PWM 簡介** 使用 Arduino 驅動發射器電路只是一個臨時方案。最好使用一些專用 IC 來實現同樣的功能（例如 [TX2C](http://www.datasheetarchive.com/pdf-datasheets/Datasheets-23/DSA-446609.html)）。**產生正確的脈衝調製** 我試圖讓 Arduino 輸出 PWM 信號，並用於驅動發射器（使用特定頻率的晶體振盪器）以開啟/關閉，從而產生所需的脈衝。根據「[如何工作](http://electronics.howstuffworks.com/rc-toy2.htm)」，RC 控制使用四個脈衝，每個脈衝長 2.1 毫秒，間隔為 700 微秒。脈衝段（告訴天線新資訊）使用 700 微秒的脈衝和 700 微秒的間隔。脈衝數量決定動作：* 前進：16 個脈衝 * 後退：40 個脈衝 * 前進/左：28 個脈衝 * 前進/右：34 個脈衝 * 後退/左：52 個脈衝 * 後退/右：46 個脈衝 此外：* RC 控制為 2.1 毫秒高電平 + 0.7 毫秒低電平（總共 2.8 毫秒）。* 這是 75% 的占空比和約 3571Hz 的頻率。* 脈衝段有 50% 的占空比（脈衝 = 間隔）和 714Hz 的頻率。使用 [Arduino PWM 教程](http://www.arduino.cc/en/Tutorial/PWM) 可以指定占空比和持續時間，但需要一種控制頻率的方法。Arduino（具體來說是 ATmega168）具有 16MHz 時鐘和分頻器（1、8、64、256 或 1024），這些分頻器將其劃分為計時器。精確控制是通過 ICR 中的整數來實現的。微控制器計數到 ICR，然後計數到 0，每次到達 0 時變為高電平。公式為：目標頻率 = 系統時鐘 / (2 * 分頻器 * ICR)。對於 2.8 毫秒的脈衝：* 16MHz / (2 * 分頻器 * ICR) = 3571Hz。解決不同分頻器的 ICR 值：* 1：ICR = 2240 * 8：ICR = 280 * 64：ICR = 35 等等。對於 1.4 毫秒的脈衝段：* 16MHz / (2 * 分頻器 * ICR) = 714Hz。計算不同分頻器的類似 ICR 值。一般來說，較高的分頻器有助於降低功耗。[ATmega 計時器教程](http://www.et06.dk/atmega_timers/) 可能會有所幫助，但我還不完全理解。**如何在 Arduino 中編寫代碼？** 我不確定。我嘗試過使用延遲手動創建 PWM，但它不起作用。購買專用 IC 並使用提供的原理圖可能更容易。"}
```". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[

A.R.T.: Autonomous Robot Toy ^\_^

Some theory gleaned related to PWM and RF

_Disclaimer: this is my first contact with PWM and RF... Feel free to correct me._

**General PWM introduction**

Using the Arduino to do drive the transmitter circuit would be a temporary hack. Best would be to be a simple circuit using a few dedicated IC to achieve the same (specifically the [TX2C](http://www.datasheetarchive.com/pdf-datasheets/Datasheets-23/DSA-446609.html)).

**Generating correct Pulse Modulation**

I'm trying to have Arduino output a PWM that will in turn drive the transmitter (using a crystal oscillator at a specific frequency) on/off to achieve the needed pulses.

According to "[How Stuff Works](http://electronics.howstuffworks.com/rc-toy2.htm)", RC control is four pulses that are 2.1 milliseconds long, with 700-microsecond intervals.

The pulse segment, which tells the antenna what the new information is, uses 700-microsecond pulses with 700-microsecond intervals. The number of pulses will tell what order to execute:

* Forward: 16 pulses
* Reverse: 40 pulses
* Forward/Left: 28 pulses
* Forward/Right: 34 pulses
* Reverse/Left: 52 pulses
* Reverse/Right: 46 pulses

also:

* RC control is 2.1 ms HIGH + 0.7ms LOW for a total of 2.8ms.
* This represents a duty of 2.1/2.8 = 75% duty cycle and a frequency of 1/0.00028 = \~3571 Hz.
* Pulse segment duty cycle is 50% (since pulse = interval) with a frequency of 1s/1.4ms (0.7ms+0.7ms) 714Hz.

With the [Arduino, we can specify duty cycle](http://www.arduino.cc/en/Tutorial/PWM) and track a certain total duration, but we still need a way to specify frequency.

According to the Secrets of [Arduino PWM](http://arduino.cc/en/Tutorial/SecretsOfArduinoPWM) and the [Servo PWM FAQ](http://mil.ufl.edu/~achamber/servoPWMfaq.html) the Arduino (or rather, the ATMega168 that it uses) has a 16Mhz clock with prescalers (1, 8, 64, 256, or 1024) that can divide this to a "timer". Final precise control is done by using an integer in the ICR. The microcontroller will count up to ICR and then count down back to 0, turning to HIGH everytime it gets to zero.

Can probably dig this out of the ATMega168 doc: http://www.atmel.com/dyn/resources/prod\_documents/doc2545.pdf

The equation is: desired\_frequency = system\_clock / (2\*prescaler\_value\*ICR)

(1/0.00028) = 16e6/ (2\*prescaler\*x) or x = (16e6\*2.8e-4)/(2\*prescaler)

where prescaler...

* 1: 2240
* 8: 280
* 64: 35
* 256: 8.75
* 1024: 2.1875

...we can thus use prescaler value 1,8,64 + corresponding ICR value. We cannot use 256 and 1024 because their results are fractional.

Same exercise with the pulse segment:

(1/0.0014) = 16e6 / (2\*prescaler\*x) or x = (16e6\*1.4e-3)/(2\*prescaler)

where prescaler...

* 1: 11200
* 8: 1400
* 64: 175
* 256: 43.75
* 1024: 10.9375

...we can use either 1, 8 or 64 prescaler (the other two are fractional values).

Higher prescale is better generally as lower timer also reduces power consumption.

The [ATmega timers script](http://www.et06.dk/atmega%5Ftimers/) should be useful at some point, but I don't understand the output right now...

**How do I turn this knowledge into an Arduino embedded program?**

I have no idea yet! I did try to manually create a PWM here by using sleeps:

<https://github.com/rngadam/ART/blob/master/rf%5Fcontrol/rf%5Fcontrol.pde>

...and feed that into an hacked together RF circuit based on what I could figure out from the circuit but it... obviously doesn't do much

I've come to the conclusion that buying the IC chip that does the same work and use the provided schematics... would be a lot easier...

\]\]> 
