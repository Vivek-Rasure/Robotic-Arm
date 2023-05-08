#include <Wire.h>
#include<Adafruit_PWMServoDriver.h>
Adafruit_PWMServoDriver s = Adafruit_PWMServoDriver();
#define servoMIN 250
#define servoMAX 400s
// code to input for the Application
int p = 180;
int q = 650;
int r = 250;
int a = 180;
int t = 400;
char val;
// to setup the robotic arm
void setup()
{ Serial.begin(9600);
  s.begin();
  s.setPWMFreq(60);
// for initial position of Robotic arm
       s.setPWM(2, 0, 180);
      delay(200);
      s.setPWM(4, 0, 680);
      delay(200);
      s.setPWM(5, 0, 350);
      delay(200);
      s.setPWM(7, 0, 220);
      delay(200);
      s.setPWM(11, 0, 350);
      delay(200);
}


void loop()
{  
//checking for Bluetooth input
  while (Serial.available())
  {
    val = Serial.read();
    Serial.println(val);
    //for base right movement
    if (val == 'a')
    { 
      p += 20;
      s.setPWM(2, 0, p);
}
    //for base left movement
    else if (val == 'b')
    {
      p -= 20;
      s.setPWM(2, 0, p);
    }
    //for shoulder up movement
    else if (val == 'c')
    {
     if(q<710)
    {
      q += 25;
      s.setPWM(4, 0, q);
      }  
  }

//for shoulder down movement
    else if (val == 'd')
    {  
      if(q>350)
    {
      s.setPWM(4, 0, q); 
     } 
}
// for elbow up movement
    else if (val == 'e')
    { 
        r -= 20;
         s.setPWM(5, 0, r);
    }
// for elbow down movement
    else if (val == 'f')
    { 
      r += 20;
      s.setPWM(5, 0, r);
    }
// for wrist up movement
    else if (val == 'g')
    {
      a += 20;   
      s.setPWM(7, 0, a);
    }
// for wrist down movement
    else if (val == 'h')
    { 
      a -= 20;
      s.setPWM(7, 0, a); 
   }
//to open the gripper 
    else if (val == 'i')
    {
       t -= 20;
      s.setPWM(11, 0, 350);
    }
// to close the gripper 
    else if (val == 'j')
    { 
      t -= 20;
      s.setPWM(11, 0, 160);    }
// to reset the robotic arm    
else if (val == 'k')    
{
      s.setPWM(2, 0, 180);
      delay(100);
      s.setPWM(4, 0, 680);
      delay(100);
      s.setPWM(5, 0, 350);
      delay(100);
      s.setPWM(7, 0, 220);
      delay(100);
      s.setPWM(11, 0, 350);
      delay(100);
    }  
  }
}
