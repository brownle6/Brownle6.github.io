---
title: "Syringe Pump Project"
excerpt: "A DIY, cost-effective alternative to expensive, entry-level modeled commercial variants. Capable of 1 uL / min flow rate up to 10 mL / min"
header:
  image: /assets/img/syringe-pump-project.png  
teaser: /assets/img/syringe-pump-project.png 
gallery:
  - image_path: /assets/img/Carriage.png
  - image_path: /assets/img/End-Support.png
  - image_path: /assets/img/Enclosure.png
  - image_path: /assets/img/Enclosure-Lid.png
  - image_path: /assets/img/Remote-Box.png
  - image_path: /assets/img/Remote-Box-Lid.png

---

# Purpose/Features of the Design

* **Purpose:** Syringe pumps are motorized devices that mechanically insert a plunger to control fluid dispensation from a syringe. Many use stepper motors to precisely move the platform attached to the syringe's plunger while another platform holds the body steady. Basic syringe pumps simply dispense liquid at a set rate controlled by the speed of the motor. Still, more sophisticated and expensive models are programmable and offer more control over the motion of the syringe. Syringe pumps are used medically to administer medication at a constant speed over long periods of time and in laboratories to perform complex routines and move small volumes of liquid with great precision. Given their typical price and ultimately simple design, syringe pumps are the ideal project for an efficient do-it-yourself alternative, especially with some knowledge of 3D printing and electrical prototyping.
* **Features of the Design:** The given constraints the syringe pump needed to meet were that it must be driven by a stepper motor rotating a lead screw. The design should be able to accommodate a 10 mL and 20 mL syringe pump without requiring any special tools for changing the size of the syringe and prevent sagging during motion. Furthermore, for the electrical components, the design must include a latching button to start and pause the motion of the pump, as well as a limit switch to stop the motion once the plunger reaches its limit. The flow rate of the pump must also be easily adjustable in the Arduino program. There must also be an LED that turns green to indicate the pump is running, yellow when pauses, and red when fully plunged. The electrical wiring for these components and the breadboard must be protected from the user and the potential spillage of liquids. All the elements must be assembled into one unit, and must be fit together using only fasteners and non-permanent snap fits. There must also be some element of unique branding to distinguish the design. Practical limitations include that components like the motor mounting plate must be able to withstand high temperatures from the stepper motor and be strong enough to support the motion. This indicated that ABS should be used for these components, which makes for longer print times than PLA. Furthermore, for ease of adjusting the electrical components, the electrical box must be easy to open and close. This especially comes into play for incorporating the optional elements and preparing the original design for ability to improve and expand functionality. However, the syringe pump must still be a single, stable unit that stays together when lifted by the pump holding components. 

# Instructions for Pump Usage

* **Step 1:** Place 10 mL or 20 mL in corresponding holes. The 10 mL holes are on the front side of the pump, and the 20 mL holes are towards the back side.
* **Step 2:** Press the black button, third from the left, to start the motion of the pump at 5 mL/min for a 20 mL syringe. To pause, press this button again. Motion will automatically stop when the syringe is empty.
* **Step 3:** To adjust the motion for a 10 mL syringe, press the red button directly to the right of the black button (the fourth button from the left).
* **Step 4:** Press and hold the first button to manually move forward. Press and hold the second button to manually move backward.
* **Step 5:** To set the speed using the knob, press the rightmost red button (5th from the left) and rotate the knob right to increase speed and left to decrease speed.
* **Step 6:** Due to prototyping limitations, the remote must be powered using a micro USB cable connected to a laptop or similar device. For future iterations, the remote will have a stand-alone power source. To turn on the syringe, flip the switch to the on position. To pause the syringe, flip it to the off position. 

# CAD Model
<iframe src="https://vanderbilt643.autodesk360.com/shares/public/SH286ddQT78850c0d8a41d57d79980bb9458?mode=embed" width="640" height="480" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true"  frameborder="0"></iframe>

# Hyperlink to Arduino Code
<a
// Libary
#include <AccelStepper.h>
#include <LiquidCrystal_I2C.h>
// pins
#define size 2 //interupt pin for changing size
#define step 10 // step pin for stepper controller
#define dir 11 // direction pin for stepper controller
#define emergency 3 // interput pin for stopping at end of travel path
#define controlbutton 4 // start pause
#define greenLED 5 // connected to green pin on led
#define redLED 6 // connected to red pin on led
#define esp 7 // connected to esp32 for remote control
#define flowrate_but 8 // controls whether flowrate is controlled by potentiometer
#define forward 12 // manual forward
#define backward 13 // manual reverse
int analog = A0; // reading potentiometer
int read = 0; // potentiometer value
double speed; // speed set by potentiometer
double speed_s; //set program speed
volatile bool sizeChangeFlag = false; //interupt contingency
volatile bool estop = false; // interupt contingency
unsigned long lastLCDUpdate = 0; // Variable to track the last update time
const unsigned long lcdInterval = 1000; // Update LCD every 1 second

// flowrate
#define flowrate 5 // mL
#define twenty_mL 2.28018 // volume pushed per revolution
#define ten_mL 1.40992 // volume pushed per revolution
#define microstep 3200.00 //microstep resolution

AccelStepper stepper(AccelStepper::DRIVER, step, dir); //initialize stepper motor

LiquidCrystal_I2C lcd(0x27,16,2); //contact lcd screen

void setup() {
 
  //pins
  pinMode(controlbutton, INPUT_PULLUP);
  pinMode(greenLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(esp, INPUT_PULLUP);
  pinMode(emergency, INPUT_PULLUP);
  pinMode(flowrate_but, INPUT_PULLUP);
  pinMode(forward, INPUT_PULLUP);
  pinMode(backward, INPUT_PULLUP);
  pinMode(size, INPUT_PULLUP);

  //interupt
  attachInterrupt(digitalPinToInterrupt(emergency), eStopISR, FALLING);
  attachInterrupt(digitalPinToInterrupt(size), sizeChangeISR, CHANGE);

  stepper.setMaxSpeed(1000); // set maximum stepper motor
  speed_s = (microstep/60) * (flowrate/twenty_mL);
  speed = speed_s;
 
  lcd.init();
  lcd.clear();        
  lcd.backlight();      // Make sure backlight is on
 
  // Welcome message
  lcd.setCursor(3,0);   //Set cursor to character 2 on line 0
  lcd.print("Welcome ||");
  lcd.setCursor(11,1);   //Move cursor to character 2 on line 1
  lcd.print("_/");

//Serial.begin(9600); // debugging purposes

delay(5000); //start up
}

void loop() {
  int i = 0;
  int j;
// start/pause function
  while (digitalRead(controlbutton) == LOW && digitalRead(emergency)==HIGH) {
    ++i;
    stepper.runSpeed();
    digitalWrite(greenLED, 1);
    digitalWrite(redLED, 0);
    if (i==1) {
    lcd.clear();
    lcd.setCursor(1,0);   //Set cursor to character 2 on line 0
    lcd.print("Moving Forward");
    }
  }
  // start/pause function remote
  while (digitalRead(esp) == LOW && digitalRead(emergency)==HIGH) {
    ++i;
    stepper.runSpeed();
    digitalWrite(greenLED, 1);
    digitalWrite(redLED, 0);
    if (i==1) {
    lcd.clear();
    lcd.setCursor(1,0);   //Set cursor to character 2 on line 0
    lcd.print("Moving Forward");
    }

  }
  // idle control, moving forward or backward
  if (digitalRead(esp) == HIGH && digitalRead(controlbutton) == HIGH && digitalRead(emergency) == HIGH) {
   
    //idle
    digitalWrite(greenLED, 1);
    digitalWrite(redLED, 1);
    //manual forward control
    while (digitalRead(forward) == LOW && digitalRead(emergency)==HIGH) {
      ++i;
      stepper.setSpeed(600);
      stepper.runSpeed();
      digitalWrite(greenLED, 1);
      digitalWrite(redLED, 0);
    if (i==1) {
    lcd.clear();
    lcd.setCursor(4,0);   //Set cursor to character 2 on line 0
    lcd.print("Forward");
    }
    }
    i=0;
    //manual reverse, capable of being enacted in emergency stop configuration for easy rewinding
    while (digitalRead(backward) == LOW) {
      ++i;
      stepper.setSpeed(-600);
      stepper.runSpeed();
      digitalWrite(greenLED, 1);
      digitalWrite(redLED, 0);
      if (i==1) {
    lcd.clear();
    lcd.setCursor(4,0);   //Set cursor to character 2 on line 0
    lcd.print("Backward");
    }
    }
   
      unsigned long currentMillis = millis();
    if (currentMillis - lastLCDUpdate >= lcdInterval) {
    lcd.clear();
    lcd.setCursor(6,0);   //Set cursor to character 2 on line 0
    lcd.print("Idle");
        lastLCDUpdate = currentMillis; // Reset the timer
    }
  }
// control speed with potentiometer
  while(digitalRead(flowrate_but) == LOW && digitalRead(emergency)==HIGH) {
      read = analogRead(analog); //read potentiomter
    double temp = read / 1024.00 * 10.0 + 1; // translate reading into mL

    // use proper size
    if (size == HIGH) {
    speed = (microstep/60.0) * (temp/twenty_mL);
    } else {
        speed = (microstep/60.0) * (temp/ten_mL);
    }
    stepper.setSpeed(speed);
 
    // run speed if pressed
    if(digitalRead(controlbutton)==LOW) {
      stepper.runSpeed();
      digitalWrite(greenLED, 1);
      digitalWrite(redLED, 0);
    }
    unsigned long currentMillis = millis();
    if (currentMillis - lastLCDUpdate >= lcdInterval) {
        lcd.clear();
        lcd.setCursor(4, 0); // Set cursor position
        lcd.print("speed(mL)");
        lcd.setCursor(6, 1); // Set cursor position
        lcd.print(temp);
        lastLCDUpdate = currentMillis; // Reset the timer
    }
  }

  //go backward at any point including after an emergency stop
  i=0;
  while (digitalRead(backward) == LOW) {
      ++i;
      stepper.setSpeed(-600);
      stepper.runSpeed();
      digitalWrite(greenLED, 1);
      digitalWrite(redLED, 0);
      if (i==1) {
    lcd.clear();
    lcd.setCursor(4,0);   //Set cursor to character 2 on line 0
    lcd.print("Backward");
    }
  }

// return to embedded preset speed
  if(digitalRead(flowrate_but) == HIGH) {
    stepper.setSpeed(speed_s);
  }

// interupt for size change
  if (sizeChangeFlag) {
    sizeChange(); // Call the function when the flag is set
    delay(3500);
    sizeChangeFlag = false; // Reset the flag
  }

// interupt for emergency stop
  if (estop) {
    outOfLiquid();
    estop = false; // Reset the flag
  }
}

// reset interupt flags
void sizeChangeISR() {
  sizeChangeFlag = true; // Set the flag
}
void eStopISR() {
  estop = true; // Set the flag
}

// procedure for size change
void sizeChange() {
   if(digitalRead(size) == LOW && digitalRead(controlbutton)==HIGH && digitalRead(esp)==HIGH) {
    speed_s = (microstep/60) * (flowrate/ten_mL);
    lcd.clear();
    lcd.setCursor(4,0);
    lcd.print("size(mL):");
    lcd.setCursor(7,1);
    lcd.print("10");
  }
   if (digitalRead(size) == HIGH && digitalRead(controlbutton)==HIGH && digitalRead(esp)==HIGH){
    speed_s = (microstep/60) * (flowrate/twenty_mL);
    lcd.clear();
    lcd.setCursor(4,0);
    lcd.print("size(mL):");
    lcd.setCursor(7,1);
    lcd.print("20");
  }
}

// emergency stop
void outOfLiquid() {
  int i = 0;
  stepper.stop();
  digitalWrite(greenLED, 0);
  digitalWrite(redLED, 1);
  lcd.clear();
  lcd.setCursor(6,0);
  lcd.print("STOP");
  lcd.setCursor(2,1);
  lcd.print("Out of Fluid"); // Call the function when the flag is set

  // stay trapped in emergency stop until system is paused
  // note that system can be reversed in this state
  while (digitalRead(esp) == LOW || digitalRead(controlbutton) == LOW) {
    stepper.stop();
    unsigned long currentMillis = millis();
    if (currentMillis - lastLCDUpdate >= lcdInterval) {
        lcd.clear();
    lcd.setCursor(6,0);
    lcd.print("STOP");
    lcd.setCursor(2,1);
    lcd.print("Out of Fluid"); // Call the function when the flag is set
        lastLCDUpdate = currentMillis; // Reset the timer
    }
    }
  }
a>

# Off-the-Shelf Parts Required

| Part | Quantity Required |
| :-- | :-- |
| 250 mm lead screw with 2 mm pitch and 2 mm lead | 1 |
| 250 mm lead screw with 2 mm pitch and 8 mm lead | 1 | 
| 1/4" x 8mm Flexible Coupling | 1 |
| 200 mm linear rod with 8 mm diameter | 2 |
| LM8UU linear bearing for 8 mm diameter rod | 2 |
| 2040 aluminum extrusion 1' length | 1 | 
| nema 17 stepper motor | 1 | 
| MEAN WELL RQ-65D AC-DC power supply quad output 5V 12V 24V 12V 4 Amp | 1 | 
| Arduino Uno | 1 | 
| A4988 Stepper Driver | 1 | 
| small breadboard | 1 | 
| panel mount latching push buttons (on/off | 1 | 
| panel mount momentary push buttons | 1 |
| limit switch | 1 | 
| RBG common cathode LED | supplied by group |

# 3D Printed Parts Required

| Part | Quantity Required |
| :-- | :-- |
| Carriage | 1 | 
| Motor Mounting Plate | 1 | 
| Syringe End Support | 1 | 
| Regular End Support | 1 | 
| Enclosure | 1 | 
| Enclosure Lid | 1 |
| Remote Box Lid | 1 | 
| Remote Box | 1 | 

{% include gallery caption="Dimensioned Drawings" %}
