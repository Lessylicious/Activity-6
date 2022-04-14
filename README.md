# Activity-6
/*Activity:6
Create a distance measuring device that:
1. turn RED LED light and Buzzer ON if distance is below 10cm;
2. turn Yellow LED light if distance is below 11cm-20cm
3. turn Green LED light if distance is more than 20cm
Distance information should be shown in LCD screen*/

//Lester Calub BSIT 2B

#include <LiquidCrystal.h> 
#define buzzer 3
LiquidCrystal lcd(1, 2, 4, 5, 6, 7); // Creates an LCD object. Parameters: (rs, enable, d4, d5, d6, d7)

const int trigPin = 11;
const int echoPin = 12;
const int red=10;
const int blue=9;
int green=8;

long duration;
float cm;
float inches;

void setup() {
  
lcd.begin(16,2); // Initializes the interface to the LCD screen, and specifies the dimensions (width and height) of the display
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(buzzer, OUTPUT);

}

void loop() {
  
digitalWrite(trigPin, LOW);
delayMicroseconds(5);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);
cm = (duration/2) / 29.1;
inches = (duration/2) / 74;

lcd.setCursor(0,0); // Sets the location at which subsequent text written to the LCD will be displayed
lcd.print("D= "); // Prints string "Distance" on the LCD
lcd.print(cm); // Prints the distance value from the sensor
lcd.print(" cm");
delay(10);
lcd.setCursor(0,1);
lcd.print("D= ");
lcd.print(inches);
lcd.print(" inch");
delay(10);

  
  if(cm<10){
    digitalWrite(red,HIGH);
    digitalWrite(green,LOW);
    digitalWrite(blue,LOW);
    digitalWrite(buzzer,HIGH);
  }
   if (cm>11 && cm<20){
    digitalWrite(red,LOW);
    digitalWrite(green,LOW);
    digitalWrite(blue,HIGH); 
     digitalWrite(buzzer,LOW);
  }
  
  if (cm > 20){
    digitalWrite(red,LOW);
    digitalWrite(green,HIGH);
    digitalWrite(blue,LOW);
    digitalWrite(buzzer,LOW);
 
  
  
  }
 
}

