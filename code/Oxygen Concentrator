//#include <Servo.LOW>
//Servo myservo;
//void SERVOMOTOR(void);

unsigned char set1=16;   //D0 First set of three pumps
unsigned char set2=4;   // D1 Second set of three pumps
unsigned char oxyvalve=5; //D2

unsigned char oxyvalve2=0; //D3 //Oxygen Valve
unsigned char oxyvalve3=2; //D4 //Oxygen Valve 4

unsigned char pressurepump=14; //D5 
unsigned char fan=12; //D6

//int pos = 0;



void setup()
{
  pinMode(set1,OUTPUT);  //Set 1 is set as OUTPUT
  pinMode(set2,OUTPUT);  //Set 2 is set as OUTPUT
  pinMode(oxyvalve,OUTPUT);  //Oxygen Valve is set as OUTPUT
  pinMode(oxyvalve2,OUTPUT);
  pinMode(oxyvalve3,OUTPUT);//Oxygen Valve is set as OUTPUT
  pinMode(pressurepump,OUTPUT);  // pressurepump is set as OUTPUT
  pinMode(fan,OUTPUT);    //fan is set as OUTPUT
}

void loop()
{
  digitalWrite(set1,LOW);  //Set 1 is ON
  digitalWrite(oxyvalve,HIGH);  //Oxygen Valve is OFF
   delay(9000);   //Delay time 1 minute 20 seconds
  
 digitalWrite(set1,HIGH);  //Set 1 is ON
digitalWrite(oxyvalve,LOW);//Oxygen Valve is ON
  digitalWrite(pressurepump,LOW);//Pressure Pump is ON
  delay(4500);   //Delay time 3 seconds
  digitalWrite(oxyvalve,HIGH);//Oxygen Valve is OFF
   digitalWrite(pressurepump,HIGH);//Pressure Pump is OFF
  delay(1000);
  OXYVALVE();
  }



void OXYVALVE(void) 
 {
  digitalWrite(oxyvalve3,LOW);  //Oxygen Valve is OFF
 digitalWrite(set2,LOW);  //Set 2 is ON
  digitalWrite(oxyvalve2,HIGH);//Oxygen Valve is OFF
 delay(9000);   //Delay time 9 seconds
 digitalWrite(set2,HIGH);  //Set 2 is ON
  digitalWrite(oxyvalve2,LOW);  //Oxygen Valve is ON
  digitalWrite(pressurepump,LOW);//Pressure Pump is ON
  
  delay(4500);   //Delay time 4.5 seconds
  digitalWrite(oxyvalve2,HIGH);  //Oxygen Valve is OFF
  digitalWrite(pressurepump,HIGH);//Pressure Pump is OFF

digitalWrite(oxyvalve3,HIGH);//Oxygen Valve is ON

  
}

  
Code For Purity of Oxygen:
//ADS1050 12 bit ADC
#include <Wire.h>
#include <Adafruit_ADS1015.h>
Adafruit_ADS1015 ads;     /* Use thi for the 12-bit version */

//Nokia Display 
#include <SPI.h>
#include <Adafruit_GFX.h>
#include <Adafruit_PCD8544.h>

// Hardware SPI (faster, but must use certain hardware pins):
// SCK is LCD serial clock (SCLK) - this is pin 13 on Arduino Uno
// MOSI is LCD DIN - this is pin 11 on an Arduino Uno
// pin 5 - Data/Command select (D/C)
// pin 8 - LCD chip select (CS)
// pin 6 - LCD reset (RST)
 Adafruit_PCD8544 display = Adafruit_PCD8544(5, 8, 6);
// Note with hardware SPI MISO and SS pins aren't used but will still be read
// and written to during SPI transfer.  Be careful sharing these pins!


//Button and backlight pin declaration
int button1pin=3;//Calibration, Enter Button

//General Cariable setup
double  calibrationv; //used to store calibrated value
int sensorcheck=0;//to check health on sensor. If value is 0 sensor works, if value is 1 sensor out of range or not connected
int Sensor_lowrange=58;//When sensor is healthy and new it reads 58 on low
int Sensor_highrange=106;//When sensor is healthy and new it reads 106 on high
int current_function=0;
void setup(void) 
{
 Serial.begin(9600);
  pinMode(button1pin,INPUT);
//starts ADS readings
 ads.setGain(GAIN_SIXTEEN);    // 16x gain  +/- 0.256V  1 bit = 0.125mV  0.0078125mV
  ads.begin();
  calibrationv=calibrate();
  //Nokia Display Setup
  display.begin();
  // you can change the contrast around to adapt the display
  // for the best viewing!
  display.setContrast(50);
    if ((calibrationv > Sensor_highrange) || (calibrationv < Sensor_lowrange))
   {
    sensorcheck=1;
     current_function=1;//Sensor needs to be calibrated
     need_calibrating();//print need calibrating message
   } 
}
//Prints need calibrating text
void need_calibrating(){
   display.clearDisplay();
  display.setCursor(0,0);
  display.setTextSize(1);
  display.setTextColor(BLACK);
  display.println("Sensor error");
  display.println("Please");
  display.println("calibrate"); 
  display.println(calibrationv);
  display.display();
  
}
//Take 20 readings and avaraging it to exclude miner diviations of hte reading
int calibrate(){
  int16_t adc0=0;
  int result;
  for(int i=0; i<=19; i++)
       {
         adc0=adc0+ads.readADC_SingleEnded(0);
       }
  
  result=adc0/20;
  return result;
}


void loop(void) {
  //********  Main Loop variable declaration *********** 
     double modr;//Variable to hold mod value in
    int16_t adc0=0;
    double result;//After calculations holds the current O2 percentage
    double currentmv; //the current mv put out by the oxygen sensor;
    double calibratev;
 
 //***** Function button read section ********  
 int button1state=digitalRead(button1pin);

 
 
  if(button1state==LOW){
    if(current_function==0){
       current_function=1;//Sensor needs to be calibrated
    }
  }
 
  switch(current_function){
   case 0://Analyzing O2
     //taking 20 samples. The sensor might spike for a millisecond. After we average the samples into one value
     for(int i=0; i<=19; i++)
       {
         adc0=adc0+ads.readADC_SingleEnded(0);
       }
      
      currentmv = adc0/20;
      calibratev=calibrationv;
      result=(currentmv/calibratev)*20.9;
      //Write to display
      display.clearDisplay();
      display.setTextSize(1);
      display.setTextColor(WHITE, BLACK);
      display.setCursor(0,0);
      display.print("O2%");
      display.setTextColor(BLACK);
      display.print(" ");
      display.setTextSize(2);
      display.println(result,1);
      display.display();
           delay(1000);
    break;
   case 1:
       display.clearDisplay();
     display.setCursor(0,0);
     display.setTextSize(1);
     display.setTextColor(WHITE,BLACK);
     display.println("Calibrating");
     display.display();
     
     current_function=0;//O2 analyzing
     calibrationv=calibrate();
     delay(2000);
      if ((calibrationv > Sensor_highrange) || (calibrationv < Sensor_lowrange)){
          current_function=1;//Sensor needs to be calibrated
          need_calibrating();//print need calibrating message
        } 
   break;
       
 }
 
}
