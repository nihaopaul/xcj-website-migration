---
id: 974
title: Use Gyro with Arduino
date: 2011-05-06 03:35:47
author: 5
---
## error
Failed to parse. Text: "```json
{"en": "The Arduino uses a gyroscope to control a servo motor.\n\nToday I got an important part of the quadcopter, the gyroscope. ^\_^ The picture below is a three-axis gyroscope, a component of the seeedstudio GROVE kit.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled1.jpg \"untitled.jpg\")\n\nThis gyroscope uses the ITG3200 chip and can be directly connected to the Arduino via the I2C interface. The default address is 0x68, but it can be changed to 0x69 by connecting JP1 on the board. The definitions of the four pins of the interface are shown in the figure below.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled2.jpg \"untitled.jpg\")\n\nYes... you didn't see it wrong, they use red as ground -\_-b\n\nThe servo motor uses the simplest PWM port. Finally, the connection is as shown in the picture below.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled3.jpg \"untitled.jpg\")\n\nI wrote a program that can make the gyroscope's rotation directly reflected on the servo arm. However, this will cause problems. When the rotation is more frequent, the servo's angle will increase until it exceeds the maximum range. This is also a less accurate place of the gyroscope. Also, when the gyroscope is stationary, the output of the z-axis is not 0, but always -1. This means the zero point of the gyroscope may be inaccurate, and the positive and negative rotations may also have differences. I don't know how much this will affect the future flight control algorithm.\n\nThe program used is shown below.\n\n```C++\n#include <Wire.h>\n#include <Servo.h>\n#define GYRO_ADDR  0x68\nServo servo;\nint currentPos;\nvoid setup()\n{\n  Wire.begin();\n  initGyro();\n  servo.attach(2);\n  currentPos = 90;\n  pinMode(3, INPUT);\n}\nvoid loop()\n{\n  int x;\n  x = readx();\n  currentPos = currentPos + x;\n  int buttonState = digitalRead(3);\n  if (buttonState == HIGH)\n  {\n    currentPos = 90;\n  }\n  servo.write(currentPos);\n}\nint readx()\n{\n  int x;\n  x = readGyro(0x1d, 0x1e);\n  return x;\n}\nchar readGyro(unsigned char addrH, unsigned char addrL)\n{\n  char ret;\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(addrH);\n  Wire.endTransmission();\n  Wire.requestFrom(GYRO_ADDR, 1);\n  ret = Wire.receive();\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(addrL);\n  Wire.endTransmission();\n  Wire.requestFrom(GYRO_ADDR, 1);\n  if (Wire.available() > 0) ret = Wire.receive() << 8;\n  return ret;\n}\nvoid initGyro()\n{\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(0x3E);\n  Wire.send(0x80);\n  Wire.endTransmission();\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(0x15);\n  Wire.send(0x00);\n  Wire.endTransmission();\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(0x16);\n  Wire.send(0x18);\n  Wire.endTransmission();\n}\n```\n\nThe Wire library is used for I2C.  Refer to the Arduino Wire library documentation for details.\n\n<http://arduino.cc/en/Reference/Wire>\n<http://v.youku.com/v_show/id_XMjYzMTg2ODQ0.html>"},"zh": "在Arduino上使用陀螺仪控制舵机\n\n今天拿到了四轴飞行器的一个重要部件，陀螺仪。^\_^ 下面图片显示的是一个三轴陀螺仪，是seeedstudio GROVE套装中的一个部件。\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled1.jpg \"untitled.jpg\")\n\n这个陀螺仪使用ITG3200芯片，可以直接通过I2C接口连接到Arduino。默认地址是0x68，可以通过连接板上的JP1更改为0x69。接口四个引脚的定义如图所示。\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled2.jpg \"untitled.jpg\")\n\n是的，你没看错，他们用红色作为地线 -\_-b\n\n舵机使用最简单的PWM接口。最终连接方式如图所示。\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled3.jpg \"untitled.jpg\")\n\n我编写了一个程序，可以使陀螺仪的旋转直接反映到舵机的摇臂上。然而，这会导致问题。当旋转频率较高时，舵机角度会增加，直到超过最大范围。这也是陀螺仪精度较低的地方。此外，当陀螺仪静止时，Z轴输出不是0，而是始终为-1。这意味着陀螺仪的零点可能不准确，正负旋转也可能有差异。我不知道这会对未来的飞行控制算法产生多大影响。\n\n使用的程序如下：\n\n```C++\n#include <Wire.h>\n#include <Servo.h>\n#define GYRO_ADDR  0x68\nServo servo;\nint currentPos;\nvoid setup()\n{\n  Wire.begin();\n  initGyro();\n  servo.attach(2);\n  currentPos = 90;\n  pinMode(3, INPUT);\n}\nvoid loop()\n{\n  int x = readx();\n  currentPos = currentPos + x;\n  int buttonState = digitalRead(3);\n  if (buttonState == HIGH)\n  {\n    currentPos = 90;\n  }\n  servo.write(currentPos);\n}\nint readx()\n{\n  int x = readGyro(0x1d, 0x1e);\n  return x;\n}\nchar readGyro(unsigned char addrH, unsigned char addrL)\n{\n  char ret;\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(addrH);\n  Wire.endTransmission();\n  Wire.requestFrom(GYRO_ADDR, 1);\n  ret = Wire.receive();\n  Wire.beginTransmission(GYRO_ADDR);\n  Wire.send(addrL);\n  Wire.endTransmission();\n  Wire.requestFrom(GYRO_ADDR, 1);\n  if (Wire.available() > 0) ret |= Wire.receive() << 8;\n  return ret;\n}\nvoid initGyro()\n{\n  // ... (陀螺仪初始化代码)\n}\n```\n\n该程序使用了Wire库来进行I2C通信。更多细节请参考Arduino Wire库文档。\n\n<http://arduino.cc/en/Reference/Wire>\n<http://v.youku.com/v_show/id_XMjYzMTg2ODQ0.html>"}
```
". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[

# 在Arduino上使用陀螺仪控制舵机

_May 1st, 2011_ 

今天拿到了四轴飞行器的一个重要部件，就是陀螺仪。^\_^ 下面这张图上的就是了，这是一个三轴陀螺仪，seeedstudio GROVE套装的一个部件。

![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled1.jpg "untitled.jpg") 

这个陀螺仪使用ITG3200芯片，可以直接使用了I2C接口连接到Arduino上面。默认的地址是0x68，但是可以修改成0x69，只要将板子上的JP1连起来就可以修改。接口四个针脚的定义就像下面这张图中所画的。

![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled2.jpg "untitled.jpg") 

是的。。你没看错，他们用红色作为地线 -\_-b

舵机就是最简单的使用pwm的口就可以了。最后链接成下面这张图中的样子。

![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled3.jpg "untitled.jpg") 

我写了一个程序，代码在下方，能够做到让陀螺仪的转动直接反应在舵机的摇臂上面。但是，这样也会遇到问题，就是当动的次数比较多的时候，舵机的角度就会越来越大，直到超过最大的范围，所以这也是陀螺仪不是很精确的地方。另外就是，在陀螺仪静止的情况下，z轴的输出不为0，始终为-1。也就是说，这个陀螺仪的零点可能是不准确的，同时，正负转动的也有可能有差别，不知道这回对将来飞控算法带来多大的影响。

最后用到的程序就是下面这段。


#include <Wire.h>
#include <Servo.h>
#define GYRO_ADDR  0x68
Servo servo;
int currentPos;
void setup()
{
  Wire.begin();
  initGyro();
  servo.attach(2);
  currentPos = 90;
  //Serial.begin(9600);
  pinMode(3, INPUT);
}
void loop()
{
  int x;
  int v;
  x = readx();
  v = ready();
  v = readz();
  currentPos = currentPos + x;
  int buttonState;
  buttonState = digitalRead(3);
  if (buttonState == HIGH)
  {
    currentPos = 90;
  }
  else
  {
    //Serial.println("LOW");
  }
  servo.write(currentPos);
}
int readx()
{
  int x;
  x = readGyro(0x1d, 0x1e);
  return x;
}
int ready()
{
  int y;
  y = readGyro(0x1f, 0x20);
  return y;
}
int readz()
{
  int z;
  z = readGyro(0x21, 0x22);
  return z;
}
char readGyro(unsigned char addrH, unsigned char addrL)
{
  char ret;
  Wire.beginTransmission(GYRO_ADDR);
  Wire.send(addrH);
  Wire.endTransmission();
  Wire.requestFrom(GYRO_ADDR, 1);
  if (Wire.available() > 0)
  {
    ret = Wire.receive();
  }
  Wire.beginTransmission(GYRO_ADDR);
  Wire.send(addrL);
  Wire.endTransmission();
  Wire.requestFrom(GYRO_ADDR, 1);
  if (Wire.available() > 0)
  {
    ret != Wire.receive()<<8;
  }
  return ret;
}
void initGyro()
{
  Wire.beginTransmission(GYRO_ADDR);
  Wire.send(0x3E);
  Wire.send(0x80);  //send a reset to the device
  Wire.endTransmission(); //end transmission
  Wire.beginTransmission(GYRO_ADDR);
  Wire.send(0x15);
  Wire.send(0x00);   //sample rate divider
  Wire.endTransmission(); //end transmission
  Wire.beginTransmission(GYRO_ADDR);
  Wire.send(0x16);
  Wire.send(0x18); // ±2000 degrees/s (default value)
  Wire.endTransmission(); //end transmission
}

程序当中Wire库就是使用I2C，具体文档可以看下面的链接。

<http://arduino.cc/en/Reference/Wire> <http://v.youku.com/v%5Fshow/id%5FXMjYzMTg2ODQ0.html>\]\]> 
