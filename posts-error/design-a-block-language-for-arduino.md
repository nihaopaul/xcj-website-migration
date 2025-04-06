---
id: 479
title: Design a Block Language for Arduino
date: 2011-02-07 01:02:43
author: 2
---
## error
Failed to parse. Text: "```json
{"en": "I have been experimenting with OpenBlocks, a flexible platform for creating new block-based languages.  Designing one for Arduino presented a choice between two approaches.\n\n### Design I\n\nFollowing the Arduino Language Reference closely results in a block language that might be overly verbose or complex, as it directly mirrors the textual code.\n\n```\nvoid setup() {\n  pinMode(1, INPUT);\n  pinMode(2, OUTPUT);\n}\nvoid loop() {\n  if (digitalRead(1) == HIGH) {\n    digitalWrite(2, LOW);\n  }\n}\n```\n\n![Design I Example](http://example.com/design1.jpg)\n\n### Design II\n\nTargeting beginners, a more intuitive approach focuses on translating user-friendly descriptions like \"When the button on pin 1 is pressed, turn on the LED on pin 2.\"  This results in a more concise and understandable block-based language.\n\n![Design II Example](http://example.com/design2.jpg)\n\nThis approach could leverage the language's metadata to infer setup code. A small runtime environment might be necessary for compilation alongside the Arduino sketch.  This is potentially worthwhile for a beginner-friendly block language.", "zh": "我一直在尝试使用 OpenBlocks，这是一个用于创建新的基于块的语言的灵活平台。为 Arduino 设计这样的语言需要在两种方法之间做出选择。\n\n### 设计 I\n\n紧密遵循 Arduino 语言参考会导致一种可能过于冗长或复杂的块语言，因为它直接反映了文本代码。\n\n```\nvoid setup() {\n  pinMode(1, INPUT);\n  pinMode(2, OUTPUT);\n}\nvoid loop() {\n  if (digitalRead(1) == HIGH) {\n    digitalWrite(2, LOW);\n  }\n}\n```\n\n![设计 I 示例](http://example.com/design1.jpg)\n\n### 设计 II\n\n针对初学者，一种更直观的方法侧重于翻译用户友好的描述，例如“当按下引脚 1 上的按钮时，打开引脚 2 上的 LED”。这导致一种更简洁、更容易理解的基于块的语言。\n\n![设计 II 示例](http://example.com/design2.jpg)\n\n这种方法可以使用语言的元数据来推断设置代码。可能需要一个小型运行时环境才能与 Arduino 草图一起进行编译。对于面向初学者的块语言来说，这可能是值得的。"}
```
". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[

I have been playing around with OpenBlocks. It's a very flexible environment to create a new block language. When it comes to design one for Arduino, I found myself wondering between two different styles of design. 

### Design I

The first design is of course to follow the [Arduino Language Reference](http://www.arduino.cc/en/Reference/HomePage) closely. However, the resulting block language seems to be a bit too "verbose?" Or should I say "busy" since it's really a graphical representation of the textual program. Here is a sample of what it looks like for the equivalence of codes here.


void setup() {
  pinMode(1, INPUT);
  pinMode(2, OUTPUT);
}
void loop() {
  if (digitalRead(1) == HIGH) {
    digitalWrite(2, LOW);
  }
}

![Vpl 1](http://139.162.84.35/wp-content/uploads/2011/02/vpl-1.jpg "vpl-1.jpg") 

### Design II

Since the block language is targeted at the beginner of Arduino and programming, most of time, we talk about "When the button on pin 1 is pushed, I want the LED on pin 2 to light up." There is a much natural way to map this statement into an intuitive block language by building the blocks around the pin. Here is how it may look like:

![Vpl 2](http://139.162.84.35/wp-content/uploads/2011/02/vpl-2.jpg "vpl-2.jpg") 

This language is more concise and easier to understand. The language itself should provide enough meta info to infer the setup codes. However, in order to do this, the language may need a little runtime (OS?) to be compiled along with the Sketch but it seems to be worth the effort. 

The OpenBlocks codes I am playing around with the idea is available at my ['ant' branch openblocks](https://github.com/taweili/openblocks/tree/ant) on github. Appreciate any feedback on this. 

\]\]> 
