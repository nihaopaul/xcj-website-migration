---
id: 158
title: First successful autonomous run of A.R.T.
date: 2010-12-27 00:44:38
author: 4
---

Today was a day of many firsts for me:
* First time I made holes in a piece of wood with a Dremel
* First time I bought tie-wraps in China
* First time I blew up the fuse for Xindanwei putting everyone in the dark when I tried to solder
* First time I've connected the Vin for an Arduino Dueminalove (instead of the external power header or USB)
* First time I've read values from an infrared sensor (E18-D80NK with a [Chinese only datasheet](http://www.61mcu.com/upload/E18-D80NK-DATASHEET-0410.pdf))
* **[First time I got an autonomous robot to be, well, autonomous - by myself!](http://www.youtube.com/watch?v=Vtc--IvJSNY) ([video](http://www.youtube.com/watch?v=Vtc--IvJSNY))**
It's neither very nice looking or very impressive when it runs, but I'm still very happy with the results. I planned something electro-mechanical with a tiny bit of embedded software all by myself (with some help from Niko with the Dremel and Héqíchén / 何琪辰 to buy the tie-wraps!). I planned, executed and... got the results I wanted! The simplistic code that I used:

const int FORWARD =  2;
const int REVERSE =  3;
const int LEFT = 4;
const int RIGHT =  5;
const int INFRARED_FORWARD = A0;
const int INFRARED_REVERSE = A1;
const int MINIMUM_INFRARED_READING = 500;
int current_reverse = LEFT;
int alt_forward = RIGHT;
char current_state;
void setup() {
  pinMode(FORWARD, OUTPUT);
  pinMode(REVERSE, OUTPUT);
  pinMode(LEFT, OUTPUT);
  pinMode(RIGHT, OUTPUT);
  pinMode(INFRARED_FORWARD, INPUT);
  pinMode(INFRARED_REVERSE, INPUT);
  Serial.begin(9600);
}
char update_state(char state, int reason) {
  char previous_state = current_state;
  if(state != current_state) {
    current_state = state;
    Serial.print(current_state);
    Serial.println(reason);
  }
  return previous_state;
}
void loop(){
    // always check if we can go forward
    int value = analogRead(INFRARED_FORWARD);
    if(value >= MINIMUM_INFRARED_READING) {
        // maybe we were correcting, so check that
        char last_state = update_state('F', value);
        digitalWrite(current_reverse, LOW);
        digitalWrite(REVERSE, LOW);
        if(last_state == 'R') {
          // we just successfully exited a bad loop, turn for a bit for half a second
          digitalWrite(alt_forward, HIGH);
          digitalWrite(FORWARD, HIGH);
          delay(1000);
          digitalWrite(alt_forward, LOW);
        }
        digitalWrite(FORWARD, HIGH);
    } else {
      // otherwise, still correcting, keep off
      digitalWrite(FORWARD, LOW);
      // we want to try to find an alt path
      int value = analogRead(INFRARED_REVERSE);
      if(value >= MINIMUM_INFRARED_READING) {
        //still have some ability to go backward
        update_state('R', value);
        digitalWrite(current_reverse, HIGH);
        digitalWrite(REVERSE, HIGH);
      } else {
        // whooaah, even backward is not possible, we're stuck
        digitalWrite(current_reverse, LOW);
        digitalWrite(REVERSE, LOW);
        update_state('S', value);
      }
    }
}

Wins:
* Wooden board and tie-wraps work exceptionally well to prototype the physical arrangement
* Using the breadboard to prototype the electronics also works well
* The Arduino "Vin" to provide current in the board header works very well (and can seamlessy switch between USB and that without resetting!)
* Sticking the RF transmitter board directly on the robot and controlling the motors with that from the Arduino works well
* The LED that comes on when an obstacle is detected by the infrared sensors is very useful for debugging (need to keep that in mind when using other sensors)
* It works!
Losses:
* Uses Alkaline AA batteries (I want to switch to the exact same Rechargeable NiCad as the car uses)
* I spent too much time working with Sketchup instead of manually testing the mechanical design first (and then Sketchup)
* There's not much around Xindanwei in terms of computer, electronic or small mechanical stores, so I should plan ahead to shop on Beijing road
* The infrared sensors that I found in the pile of stuff in Xinchejian work, but more like "on/off" sensors (don't seem to have any linearity in the distance)
* No bumper (the infrared sensor was crashing into the walls...)
* Making an obstacle course big enough is annoying
* I had forgotten to make the holes to attach the sensors (more holes == better)
* No on/off switch so have to manually remove the connections to turn off power
* You can never have enough tie-wraps... We only had four at Xinchejian before I bought a pack of 500 for 15RMB (but really, worth about 5RMB)
* I need to learn how to solder... without blowing fuses...