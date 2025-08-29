# Irrigation-Alert-System-Useing-Arduino
-It detects the moisture leval in soil and prints it on LCD (e.g: Soil is Wet).If the soil is too dry it turns on a buzzer. 
-Components Used:Soil Moisture Sensor (Analog Type), Arduino(UNO), Led(x2), LCD(I2C, Buzzer(Peizo), Breadbord(Mini), Resister(x2), Jumper Wires and power supply. 
-Problem I faced was that SCL and SDL pins were not working with useing LiquidCrystal_I2C library , so I instead used Adafruit_LiquidCrystal library (It was more easy to use and supported SDA and SCL pins.
Code:
#include <Adafruit_LiquidCrystal.h>

int seconds = 0;

Adafruit_LiquidCrystal lcd_1(0);

int ledg = 7 ;
int ledr = 8 ;
int sensor = A0;
int buzz = 4;

void setup()
{
  pinMode(buzz, OUTPUT);
  pinMode(ledr, OUTPUT);
  pinMode(ledg, OUTPUT);
  pinMode(sensor, INPUT);
  Serial.begin(9600);
  
lcd_1;
lcd_1.begin(16, 2);
lcd_1.setCursor(0,0);
lcd_1.print("Soil Moisture");
}

void loop()
{
  int moisture = analogRead(sensor);
  lcd_1.setCursor(0,1);
  
  if(moisture < 500 ){
    digitalWrite(ledr,HIGH);
    digitalWrite(buzz,HIGH);
    digitalWrite(ledg,LOW);
   lcd_1.print("Soil is dry");
    
  }else{
    digitalWrite(ledg,HIGH);
    digitalWrite(buzz,LOW);
    digitalWrite(ledr,LOW);
   lcd_1.print("Soil is wet");
  }
     Serial.println(moisture);
}




   Circuit diagram:<img width="1244" height="773" alt="image" src="https://github.com/user-attachments/assets/24601338-2553-4b10-8a29-90881be23a52" />
