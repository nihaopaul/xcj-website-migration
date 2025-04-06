---
id: 141
title: RC Transmitter reverse-engineering attempt
date: 2010-12-26 12:32:39
author: 4
---

Kind of a failed attempt, but I thought my approach was interesting. The RC remote has a board to do the control based on four contact switch (Up, Down, Left, Right). The IC on the board says "TX-2-G, A1019265". I couldn't find the datasheet or the IC online (I think this might be similar to the [TX2C](http://www.datasheetarchive.com/TX2C%20ATS302T-datasheet.html) ATS302T which is available on [Taobao](http://item.taobao.com/item.htm?id=3199233926)), so I thought I would try to figure out the circuit by looking at it. Kind of inconvenient because the components are on one side while the circuit trace is in the other. Flipping over the board constantly is annoying and it's rather hard to follow. Best would be to see both sides at the same time, no? So this is what I did:
1. took a picture of both sides in macro mode
2. cropped both pictures
3. created layers using [GIMP](http://www.gimp.org/) (a cross-platform OpenSource software similar to Photoshop)
4. Put each image on their layers
5. Change opacity of top layer
6. "Image > Transform > Flip Horizontally" one of the image
7. Move one of the image until screw holes on both align
[gallery link="file"] Much easier then to figure out what is connected to what, but still difficult... Anyway, I decided to try instead to buy a TX2C and follow its datasheet to re-create the circuit. In the meantime, I've removed the board entirely from the remote control body and I'll connect to that directly with the Arduino.