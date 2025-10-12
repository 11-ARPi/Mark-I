# Introduction
Below is a tutorial that will help you build your own robotic hand that closes and opens its fingers using an IR sensor. I named it Mark I, but you can call it whatever you want.



## Materials needed:
- 1 Arduino Uno
- 1 IR sensor
- 5 servomotors (for each finger)
- 1 or 2 breadboards
- Cables jumper
  
### Optional 
  - 1 power bank (to power the Arduino)



Mark I's code:

    #include <Servo.h>
    
    
    const int irPin1 = 10;   
    const int servo3Pin = 3;
    const int servo4Pin = 4;
    const int servo5Pin = 5;
    const int servo6Pin = 6;
    const int servo7Pin = 7;
    
    
    Servo servo3;
    Servo servo4;
    Servo servo5;
    Servo servo6;
    Servo servo7;
    
    
    int lastServo3 = -1;
    int lastServo4 = -1;
    int lastServo5 = -1;
    int lastServo6 = -1;
    int lastServo7 = -1;
    
    
    void setServo(Servo &servo, int &lastAngle, int angle){
      if(lastAngle != angle){
        servo.write(angle);
        lastAngle = angle;
        delay(15); 
      }
    }
    
    void setup() {
      pinMode(irPin1, INPUT);
    
      servo3.attach(servo3Pin);
      servo4.attach(servo4Pin);
      servo5.attach(servo5Pin);
      servo6.attach(servo6Pin);
      servo7.attach(servo7Pin);
    
     
      servo3.write(0); lastServo3 = 0;
      servo4.write(0); lastServo4 = 0;
      servo5.write(0); lastServo5 = 0; 
      servo6.write(0); lastServo6 = 0; 
      servo7.write(0); lastServo7 = 0;
    
    
    }
    
    void loop() {
      int ir1 = digitalRead(irPin1);
    
      if(ir1 == LOW){ 
        Serial.println("IR activ");
    
        setServo(servo3, lastServo3, 0); 
        setServo(servo4, lastServo4, 0); 
        setServo(servo5, lastServo5, 0);   
        setServo(servo6, lastServo6, 0);   
        setServo(servo7, lastServo7, 0); 
    
      } else { 
        Serial.println("IR inactiv");
    
        setServo(servo3, lastServo3, 180);  
        setServo(servo4, lastServo4, 180);  
        setServo(servo5, lastServo5, 180); 
        setServo(servo6, lastServo6, 180); 
        setServo(servo7, lastServo7, 180);   
      }
    }
    
    
    
