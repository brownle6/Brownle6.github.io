---
title: "Syringe Pump Project"
excerpt: "A DIY cost-effective alternative to commercial variants that cost several hundreds dollars for entry level models. Capable of 1 uL / min flow rate up to 10 mL / min"
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
