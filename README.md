# ROCK-PAPER-SCISSOR-GAME-
 This code is a basic Arduino program that uses 3 servos, and an ultrasonic sensor to create an interactive system which i have turned into a game

*Purpose of the Code:
The program uses an ultrasonic sensor to measure the distance between the sensor and an object. If the distance is less than 20 cm, one of three servo motors is randomly activated. The chosen servo motor rotates to 179 degrees, waits for 1 second, and then returns to its default position of 90 degrees.
*Key Components:-
Ultrasonic Sensor (HC-SR04):
Pins 11 (Trigger) and 10 (Echo) are used to send and receive signals.
The function checkdistance_11_10() calculates the distance to an object by measuring the time it takes for the ultrasonic wave to travel to the object and back.
Servo Motors:
Three servo motors are connected to pins 3, 6, and 9.
When triggered, the selected servo rotates to 179 degrees and then returns to 90 degrees.
Random Activation:
The global variable A is assigned a random number between 0 and 3.
Based on the value of A, one of the three servos is activated.
*Applications:
Interactive Installations: This setup could be part of an interactive system where proximity triggers movement, like waving robotic arms.
Robotics: Useful for obstacle detection and response.
Educational Projects: Demonstrates the integration of sensors and actuators with Arduino.
code:-
#include <Servo.h>
volatile long int A;
float checkdistance_11_10() 
{
digitalWrite(11, LOW);
delayMicroseconds(2);
digitalWrite(11, HIGH);
delayMicroseconds(10);
digitalWrite(11, LOW);
float distance = pulseIn(10, HIGH) / 58.00;
delay(10);
return distance;
}

Servo servo_3;
Servo servo_6;
Servo servo_9;

void setup()
{
A = 0;
pinMode(11, OUTPUT);
pinMode(10, INPUT);
servo_3.attach(3);
servo_6.attach(6);
servo_9.attach(9);
}

void loop()
{
if (checkdistance_11_10() < 20) {
A = random(0, 4);
switch (A) {
case 1:
servo_3.write(179);
delay(1000);
servo_3.write(90);
delay(500);
break;
case 2:
servo_6.write(179);
delay(1000);
servo_6.write(90);
delay(500);
break;
case 3:
servo_9.write(179);
delay(1000);
servo_9.write(90);
delay(500);
break;
}

}
}
