#include <avr/wdt.h>

//Time saved to compare
unsigned long timeOld = 0;

void setup() {
  Serial.begin(9600);
  Serial.println("Booting up...");
  delay(100);
  pinMode(13,OUTPUT);
  timeOld = millis();
  watchdogSetup();
  Serial.println("Boot up completed");
}

void loop() {
  idle_run(); // just togles led every 1000ms
}

void idle_run(){
  if (millis() > timeOld){
     digitalWrite(13, digitalRead(13));
     timeOld = millis() + 1000UL;
     wdt_reset();
  }
}

void watchdogSetup(){
  cli(); //disable all interrupts
  wdt_reset(); //reset the WDT timer
  /*
  WDTDSR configuration:
  WDIE = 1 : Interrupt Enable
  WDE  = 1 : Reset Enable
  WDP3 = 0 : Set the four prescaler bits for a 2 sec timeout
  WDP2 = 1
  WDP1 = 1
  WDP0 = 1
  */
  //Enter Watchdog Configuration mode:
  //(1<<5) generated a byte with all zeros and one 1 at the 5th (counting from zero) bit from right.
  //
  WDTCSR |= (1<<WDCE) | (1<<WDE);
  //Set watchdog settings:
  WDTCSR = (1<<WDIE) | (1<<WDE) | (0<<WDP3) | (1<<WDP2) | (1<<WDP1) | (1<<WDP0);
  sei();//Enable interupts
}





