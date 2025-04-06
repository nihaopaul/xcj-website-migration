---
id: 472
title: Visual Programming Language for Arduino (1)
date: 2011-02-05 23:08:14
author: 2
---

To make Arduino easier for non-programmers, I decided to start a visual programming environment similar to Scratch for Arduino.

### Similar Projects around the Web

Modkit is a similar project but at the time I wanted to start the project, it was in a closed alpha. Also, it seems that modkit is going to be proprietary and I want an open source VPL for Arduino. By the way, Modkit CrimpCards is an awesome idea and design.

S4A (Scratch for Arduino) is another interesting project but it's for using Scratch with Arduino instead of programming for Arduino.

David Mellis over at MIT Media Lab also has a project called "Scratch for Arduino" but no detail yet. David is also one of the creator of Arduino platform.

### Arduino IDE and OpenBlocks

Fork the source of Arduino IDE hosted on github to host my version here. Next stop is to find a library for the visual programming. I found a project called OpenBlocks developed as part of the MIT StarLogo NG. Open Blocks is also used in Google's Android development tool App Inventor.

Both Arduino IDE and Open Blocks are written in Java so the integration should be smooth. Since I have done by share of Java, I decided to also use this opportunities to look into a few alternative languages running on JVM to implement this. Since I have done mostly Ruby for the past few years, JRuby looks pretty good. The language I really want to use is Clojure but it seems it's a bit tricky to use it embedded in a Java app. Will give both a try and see how it goes.

# Let the hacking beging!

Hopefully, we will have a running version in the next few weeks.