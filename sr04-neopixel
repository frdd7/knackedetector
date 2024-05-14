#include <Adafruit_NeoPixel.h>


/*
Knäckedetector
To do:
ändra till mm
kolla om brightness är lagom
*/

/*
  Ping))) Sensor

  This sketch reads a PING))) ultrasonic
  rangefinder and returns the distance to the
  closest object in range. To do this, it sends a
  pulse to the sensor to initiate a reading, then
  listens for a pulse to return.  The length of
  the returning pulse is proportional to the
  distance of the object from the sensor.

  The circuit:
   * +V connection of the PING))) attached to +5V
   * GND connection attached to ground
   * SIG connection attached to digital pin 7

  http://www.arduino.cc/en/Tutorial/Ping

  This example code is in the public domain.
*/

// Which pin on the Arduino is connected to the NeoPixels?
// On a Trinket or Gemma we suggest changing this to 1:
#define LED_PIN    6
 
// How many NeoPixels are attached to the Arduino?
#define LED_COUNT 8
 
// Declare our NeoPixel strip object:
Adafruit_NeoPixel strip(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);
// Argument 1 = Number of pixels in NeoPixel strip
// Argument 2 = Arduino pin number (most are valid)
// Argument 3 = Pixel type flags, add together as needed:
//   NEO_KHZ800  800 KHz bitstream (most NeoPixel products w/WS2812 LEDs)
//   NEO_KHZ400  400 KHz (classic 'v1' (not v2) FLORA pixels, WS2811 drivers)
//   NEO_GRB     Pixels are wired for GRB bitstream (most NeoPixel products)
//   NEO_RGB     Pixels are wired for RGB bitstream (v1 FLORA pixels, not v2)
//   NEO_RGBW    Pixels are wired for RGBW bitstream (NeoPixel RGBW products)


// Define colors 
      uint32_t red = strip.Color(255, 0, 0);
      uint32_t green = strip.Color(0, 255, 0);
      uint32_t blue = strip.Color(0, 0, 255);
      uint32_t yellow = strip.Color(255, 255, 0);
      uint32_t aqua = strip.Color(0, 255, 255);
      uint32_t magenta = strip.Color(255, 0, 255);
	  uint32_t amber= strip.Color(180, 100, 0);
      uint32_t white = strip.Color(255, 255, 255);

int inches = 0;

int cm = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600); // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
  //strip.setBrightness(64); // brightness från 0 till 255
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}

long averageDistanceFor(int numMeasures){
  if (numMeasures <= 0) {
  	return 0;  
  }
    
  long measure = 0;
  for (int i = 0; i < numMeasures; i++) {
  	measure += 0.01723 * readUltrasonicDistance(7, 7);
  	delay(100);  
  }
  
  return measure / numMeasures;
}

void loop()
{
  // measure the ping time in cm
  cm = averageDistanceFor(3);

  Serial.print(cm);
  Serial.println("cm");

if (cm <= 10) {  
    strip.clear();
    strip.fill(green, 0, 8); // fill hela strip med grön            
    strip.show();
}
  
else if (cm > 10 && cm <= 20) { 
  	strip.clear();
	strip.fill(green,0 ,7);
	strip.show();
}
  
else if (cm > 20 && cm <= 30) { 
  	strip.clear();
	strip.fill(green,0 ,6);
	strip.show();
}
  
else if (cm > 30 && cm <= 40) { 
  	strip.clear();
	strip.fill(yellow,0 ,5);
	strip.show();
}
  
else if (cm > 40 && cm <= 50) { 
  	strip.clear();
	strip.fill(yellow,0 ,4);
	strip.show();
}
  
else if (cm > 50 && cm <= 60) { 
  	strip.clear();
	strip.fill(yellow,0 ,3);
	strip.show();
}
  
else if (cm > 60 && cm <= 70) { 
  	strip.clear();
	strip.fill(amber,0 ,2);
	strip.show();
}

else if (cm > 70 && cm <= 80) { 
  	strip.clear();
 	strip.fill(amber, 0, 1); // fill amber till pixel 1 
  	strip.show();
}
 
else if (cm > 80) { 
  	strip.clear();
 	strip.fill(red, 0, 8); // fill hela röd om mer än 80 cm 
  	strip.show();
}
                 
  delay(100); // Wait for 100 millisecond(s)
}

//  code graveyard:
//	strip.setPixelColor(6, 255, 0, 255); // neopixel 6 till nån färg
//	convert to inches by dividing by 2.54
//	inches = (cm / 2.54);
//	Serial.print(inches);
//	Serial.print("in, ");
//	if (cm <= 20) { digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
//	else if (cm > 20) { digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level);
// 	}
