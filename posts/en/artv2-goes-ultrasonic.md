---
id: 289
title: ARTv2 goes Ultrasonic!
date: 2010-12-30 23:56:02
author: 4
---

The day started with a breakfast next to ARTv2 at Xindanwei/Xinchejian. 潘先生 (aka Panda) had left me an idea on the whiteboard for how to read a continuously rotating sensor without the cables getting twisted. I then had Chinese class with Susan Dai for four hours (2 in the morning and 2 in the afternoon). When I came back, I messed around with controlling the servo for doing sensor sweeps. In the evening, during an impromptu Xinchejian show-and-tell with people having a meeting at Xindanwei, I had the following exchange:
Me: ...since we don't have many working sensors, I'm waiting for the ultrasonic sensors we ordered... BTW, Xu, any news about them?
Xu: Oh, they're at my desk!
Me: _screams like a little girl_
Xu: ... ok, I'll go get them now... So yeah, I finally got my 10 (!) ultrasonic sensors (HC-SR04) this evening, just in time as I had worked out how to control the servo to do sensor sweeps (left and right on 180 degrees). BTW, if you're a Xinchejian member, please feel free to borrow one or two to try them out. They're affordable (37RMB on Taobao or 5.60$USD), ridiculously easy to install and seem to work as advertised, although I haven't benchmarked much. I've also spent quite a bit of time this evening on a reasonably workable controller with a state machine but only had time to test it once before I had to call it a day. I can probably use more sensors (on the sweeper, sideways, looking backward), but I'm thinking that I really need to combine them with infrared sensors as there's a longer delay than infrared in detecting obstacles and they can work at angles simultaneously. Anyway, more testing and experiments are in order.