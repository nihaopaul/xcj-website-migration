---
id: 985
title: Reading g-sensor with Arduino
date: 2011-05-06 03:48:47
author: 5
---
## error
Failed to parse. Text: "```json
{"en": "Arduino reads g-sensor data\n\nOn a quadcopter, in addition to the gyroscope, another important sensor is the gravity sensor. Due to their respective errors, if a single sensor is used, it will cause serious precision problems, causing the aircraft to lose stability. Therefore, two sensors must be used for mutual correction.\n\nCurrently, gravity sensors are widely used. Smartphones such as the iPhone and even some counterfeit phones have gravity sensors.\n\nThis time, we want to use Android to read the gravity sensor data. This gravity sensor module was purchased from Taobao. The module is very simple, and you can easily buy the chip and solder it yourself. Based on its datasheet, you can learn how to use this gravity acceleration module.\n\nThe chip used in this module is the MMA7260Q (datasheet [download](promotion/download/25270%5FMOTOROLA%5FMMA7260Q.pdf) [PDF, 229KB]). The circuit used in the test is as shown in the figure below.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled8.jpg \"untitled.jpg\")\n\nThe goal of control is to control the servo motor rotation based on the gravity sensor data. However, there is still some jitter. A simple filter was added to the program. The order was not carefully adjusted, but it can basically achieve control.\n\n<http://v.youku.com/v_show/id_XMjYzNjIyODIw.html>\n\nThe following are close-ups of the chip.\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled9.jpg \"untitled.jpg\") ![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled10.jpg \"untitled.jpg\")\n\nThe following is the code used:\n\n```C++\n#include <Servo.h>\n//Author:  HE Qichen\n//Email:  heqichen@gaishi.vicp.net\n//Website:  http://gaishi.vicp.net\n//Date:  2011-5-2\n#define FILTER_LEVEL  3\nclass Filter\n{\n  private:\n    int buffer[FILTER_LEVEL];\n  public:\n    Filter()\n    {\n      for (int i = 0; i < FILTER_LEVEL; ++i)\n        buffer[i] = 0;\n    }\n    int filter(int value)\n    {\n      int sum = 0;\n      for (int i = FILTER_LEVEL - 1; i > 0; --i)\n        buffer[i] = buffer[i - 1];\n      buffer[0] = value;\n      for (int i = 0; i < FILTER_LEVEL; ++i)\n        sum += buffer[i];\n      return sum / FILTER_LEVEL;\n    }\n};\nServo testServo;\nFilter xFilter, yFilter, zFilter;\nvoid setup()\n{\n  Serial.begin(9600);\n  testServo.attach(2);\n}\nvoid loop()\n{\n  int gx, gy, gz;\n  gx = analogRead(A0);\n  gy = analogRead(A1);\n  gz = analogRead(A2);\n  Serial.print(\"x: \");\n  Serial.print(gx, DEC);\n  Serial.print(\"  y: \");\n  Serial.print(gy, DEC);\n  Serial.print(\"  z: \");\n  Serial.println(gz, DEC);\n  int fgx, fgy, fgz;\n  fgx = xFilter.filter(gx);\n  fgy = yFilter.filter(gy);\n  fgz = zFilter.filter(gz);\n  Serial.print(\"  fx: \");\n  Serial.print(fgx, DEC);\n  Serial.print(\"  fy: \");\n  Serial.print(fgy, DEC);\n  Serial.print(\"  fz: \");\n  Serial.println(fgz, DEC);\n  testServo.write((fgz - 100) / 3);\n}\n```"},"zh": "Arduino 读取 g-传感器数据\n\n四轴飞行器除了陀螺仪外，重力传感器也是一个重要的传感器。由于它们各自的误差，使用单一传感器会造成严重的精度问题，使飞行器失去稳定性。因此需要使用两个传感器进行相互校正。\n\n目前重力传感器应用非常广泛，包括 iPhone 等智能手机以及一些山寨手机都配备了重力传感器。\n\n这次要使用 Arduino 读取重力传感器的读数。这个重力传感器模块是从淘宝购买的，模块非常简单，用户可以自行购买芯片并焊接。根据其数据手册，可以了解如何使用这个重力加速度模块。\n\n该模块使用 MMA7260Q 芯片（数据手册 [下载](promotion/download/25270%5FMOTOROLA%5FMMA7260Q.pdf) [PDF, 229KB]）。测试中的电路如图所示：\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled8.jpg \"untitled.jpg\")\n\n控制目标是根据重力传感器的读数来控制舵机的转动。但观察到存在少量抖动，因此程序中加入了一个简单的滤波器。滤波器阶数没有仔细调整，但基本上能够实现控制。\n\n<http://v.youku.com/v_show/id_XMjYzNjIyODIw.html>\n\n以下是一些芯片的细节照片：\n\n![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled9.jpg \"untitled.jpg\") ![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled10.jpg \"untitled.jpg\")\n\n以下是使用的代码：\n\n```C++\n#include <Servo.h>\n// 作者：何奇辰\n// 邮箱：heqichen@gaishi.vicp.net\n// 网站：http://gaishi.vicp.net\n// 日期：2011-5-2\n#define FILTER_LEVEL  3\nclass Filter\n{\n  private:\n    int buffer[FILTER_LEVEL];\n  public:\n    Filter()\n    {\n      for (int i = 0; i < FILTER_LEVEL; ++i)\n        buffer[i] = 0;\n    }\n    int filter(int value)\n    {\n      int sum = 0;\n      for (int i = FILTER_LEVEL - 1; i > 0; --i)\n        buffer[i] = buffer[i - 1];\n      buffer[0] = value;\n      for (int i = 0; i < FILTER_LEVEL; ++i)\n        sum += buffer[i];\n      return sum / FILTER_LEVEL;\n    }\n};\nServo testServo;\nFilter xFilter, yFilter, zFilter;\nvoid setup()\n{\n  Serial.begin(9600);\n  testServo.attach(2);\n}\nvoid loop()\n{\n  int gx, gy, gz;\n  gx = analogRead(A0);\n  gy = analogRead(A1);\n  gz = analogRead(A2);\n  Serial.print(\"x: \");\n  Serial.print(gx, DEC);\n  Serial.print(\"  y: \");\n  Serial.print(gy, DEC);\n  Serial.print(\"  z: \");\n  Serial.println(gz, DEC);\n  int fgx, fgy, fgz;\n  fgx = xFilter.filter(gx);\n  fgy = yFilter.filter(gy);\n  fgz = zFilter.filter(gz);\n  Serial.print(\"  fx: \");\n  Serial.print(fgx, DEC);\n  Serial.print(\"  fy: \");\n  Serial.print(fgy, DEC);\n  Serial.print(\"  fz: \");\n  Serial.println(fgz, DEC);\n  testServo.write((fgz - 100) / 3);\n}\n```"}
```". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[

# Arduino读取g-sensor数据

_May 2nd, 2011_ 

在四轴飞行器上除了要有陀螺仪外，还要有个重要的传感器就是重力传感器。由于它们各自的误差，若使用单一的传感器会造成严重的精读问题，使飞行器丧失稳定性。所以要用两个传感器进行相互矫正。

现在重力传感器应用非常广，目前iphone等智能手机上都有重力传感器，包括笔者的一台山寨手机上都有重力传感器。

这次就是要用Android来读取重力传感器的数据。这个重力传感器模块是从淘宝购买的，模块非常简单，自己够买芯片来焊接也不成问题。根据它的datasheet，就能够知道如何使用这款重力加速度模块了。下面就进行详细的介绍

这个模块使用的芯片型号是MMA7260Q，(datasheet[下载](promotion/download/25270%5FMOTOROLA%5FMMA7260Q.pdf)\[PDF,229KB\])，测试中的电路就是下面图片中的样子

![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled8.jpg "untitled.jpg") 

控制的目标是通过重力传感器的数据来控制舵机的转动。但是发现会有少量的抖动，于是在程序中加入了一个简单的滤波器，阶数没有仔细调，但是基本上能够进行控制了。

<http://v.youku.com/v%5Fshow/id%5FXMjYzNjIyODIw.html> 

下面是芯片的特写

![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled9.jpg "untitled.jpg") ![Untitled](http://139.162.84.35/wp-content/uploads/2011/05/untitled10.jpg "untitled.jpg") 

下面是用到的代码


#include <Servo.h>
//Author:  HE Qichen
//Email:  heqichen(a)gaishi.vicp.net
//Website:  http://gaishi.vicp.net
//Date:  2011-5-2
#define FILTER_LEVEL  3
class Filter
{
  private:
    int buffer[FILTER_LEVEL];
  public:
    Filter()
    {
      int i;
      for (i=0; i<FILTER_LEVEL; ++i)
      {
        buffer[i] = 0;
      }
    }
    int filter(int value)
    {
      int i;
      int sum;
      for (i=0; i<FILTER_LEVEL-1; ++i)
      {
        buffer[i] = buffer[i+1];
      }
      buffer[FILTER_LEVEL-1] = value;
      sum = 0;
      for (i=0; i<FILTER_LEVEL; ++i)
      {
        sum += buffer[i];
      }
      return sum / FILTER_LEVEL;
    }
};
Servo testServo;
Filter xFilter, yFilter, zFilter;
void setup()
{
  Serial.begin(9600);
  testServo.attach(2);
}
void loop()
{
  int gx, gy, gz;
  gx = analogRead(A0);
  gy = analogRead(A1);
  gz = analogRead(A2);
  Serial.print("x: ");
  Serial.print(gx, DEC);
  Serial.print("  y: ");
  Serial.print(gy, DEC);
  Serial.print("  z: ");
  Serial.println(gz, DEC);
  int fgx, fgy, fgz;
  fgx = xFilter.filter(gx);
  fgy = yFilter.filter(gy);
  fgz = zFilter.filter(gz);
  Serial.print("  fx: ");
  Serial.print(fgx, DEC);
  Serial.print("  fy: ");
  Serial.print(fgy, DEC);
  Serial.print("  fz: ");
  Serial.println(fgz, DEC);
  testServo.write((fgz-100)/3);
  //delay(10);
}

\]\]> 
