---
title: "Syringe Pump Project from DF-2100"
excerpt: "A designed, programmed, 3D-printed, and cost effective alternative to commercial variants that cost several hundreds dollars for entry level models."
header:
  image: /assets/img/syringe-pump-project.png  
teaser: /assets/img/Large-Format-3D-Printer-Thumbnail.png
gallery:
  - image_path: assets/img/Slide-3.png
  - image_path: assets/img/Slide-2.png
  - image_path: assets/img/Slide-4.png
   
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

{% include gallery caption="Large Format 3D Printer Gallery" %}
