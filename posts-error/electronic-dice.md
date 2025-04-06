---
id: 501
title: Electronic Dice
date: 2011-02-27 11:31:02
author: 2
---
## error
Failed to parse. Text: "```json
{"en": "Got a chance to introduce Arduino to the boy scout at YCIS. It was a fun afternoon working with the boys and the parents. Here are more on the design of the electronic dice. Look forward to seeing the boys completing the system next week.\n\nThe tool used to design the dice is [Fritzing](http://fritzing.org). It's an open source design program for interactive electronics. The functionalities of the dice is pretty straight forward: when the button is pressed, the LEDs start to flash and on the release of the button, one of the LED is randomly picked.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled.jpg \"untitled.jpg\")\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled1.jpg \"untitled.jpg\")\n\n[Arduino](http://arduino.cc) is used to drive the dice logics. Arduino is a popular open source microcontroller for building interactive electronics. It comes with an easy-to-use IDE that can be downloaded [here.](http://arduino.cc/en/Main/Software)\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled2.jpg \"untitled.jpg\")\n\nThe complete program of the dice is here. Just connect up the Arduino board to the computer using the USB cable and launch the IDE to upload the program. Would be fun to see some tinkering with the program to provide different behavior of the dice.\n\n```C++\n#define RANDOM 1\n#define PICKED 2\n#define BOUNCEDELAY 50\nint state;\nvoid setup()\n{\n  pinMode(7, INPUT);\n  pinMode(2, OUTPUT);\n  pinMode(3, OUTPUT);\n  pinMode(4, OUTPUT);\n  state = 1;\n  Serial.begin(9600);\n}\nint reading = 0;\nint button = 0;\nint last_button = 0;\nint picked = 0;\nvoid loop()\n{\n  if (state == RANDOM) {\n    digitalWrite(2, HIGH);\n    digitalWrite(3, LOW);\n    digitalWrite(4, LOW);\n    delay(50);\n    digitalWrite(2, LOW);\n    digitalWrite(3, HIGH);\n    digitalWrite(4, LOW);\n    delay(50);\n    digitalWrite(2, LOW);\n    digitalWrite(3, LOW);\n    digitalWrite(4, HIGH);\n    delay(50);\n  } else if (state == PICKED) {\n    digitalWrite(2, LOW);\n    digitalWrite(3, LOW);\n    digitalWrite(4, LOW);\n    digitalWrite(picked, HIGH);\n  }\n  reading = digitalRead(7);\n  if (reading != last_button) {\n    last_button = reading;\n    button = reading;\n  }\n  if (button == HIGH) {\n    state = RANDOM;\n  } else {\n    state = PICKED;\n    if (button != last_button) {\n      picked = random(3) + 2;\n    }\n  }\n}\n```", "zh": null}
```
". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[

Got a chance to introduce Arduino to the boy scout at YCIS. It was a fun afternoon working with the boys and the parents. Here are more on the design of the electronic dice. Look forward to seeing the boys completing the system next week. 

The tool used to design the dice is [Fritzing](http://fritzing.org). It's an open source design program for interactive electronics. The functionalities of the dice is pretty straight forward: when the button is press, the LEDs start to flash and on the release of the button, one of the LED is randomly picked.

![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled.jpg "untitled.jpg")

![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled1.jpg "untitled.jpg") 

[Arduino](http://arduino.cc) is used to drive the dice logics. Arduino is a popular open source microcontroller for building interactive electronics. It comes with an easy-to-use IDE that can be downloaded [here.](http://arduino.cc/en/Main/Software) 

![Untitled](http://139.162.84.35/wp-content/uploads/2011/02/untitled2.jpg "untitled.jpg") 

The complete program of the dice is here. Just connect up the Arduino board to the computer using the USB cable and launch the IDE to upload the program. Would be fun to see some tinkering with the program to provide different behavior of the dice. 

```

#define RANDOM 1
#define PICKED 2
#define BOUNCEDELAY 50
int state;
void setup()
{
  pinMode(7, INPUT);
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  state = 1;
  Serial.begin(9600);
}
int reading = 0;
int button = 0;
int last_button = 0;
int picked = 0;
void loop()
{
  if (state == RANDOM) {
    digitalWrite(2, HIGH);
    digitalWrite(3, LOW);
    digitalWrite(4, LOW);
    delay(50);
    digitalWrite(2, LOW);
    digitalWrite(3, HIGH);
    digitalWrite(4, LOW);
    delay(50);
    digitalWrite(2, LOW);
    digitalWrite(3, LOW);
    digitalWrite(4, HIGH);
    delay(50);
  } else if (state == PICKED) {
    digitalWrite(2, LOW);
    digitalWrite(3, LOW);
    digitalWrite(4, LOW);
    digitalWrite(picked, HIGH);
  }
  reading = digitalRead(7);
  if (reading == last_button) {
    button = reading;
  } else {
   last_button = reading;
  }
  if (button == 1) {
    state = RANDOM;
  } else {
    state = PICKED;
    if (button != last_button) {
      picked = random(3) + 2;
    }
  }
}

```

\]\]> 
