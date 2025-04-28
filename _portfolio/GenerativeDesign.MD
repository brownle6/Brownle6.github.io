---
title: "Generatively Designed Lacrosse Stick Head"
excerpt: "A powder printed lacrosse stick head functionally lightweighted through generative design"
header:
  image: /assets/img/mainimagelacrosse.png  
teaser: /assets/img/mainimagelacrosse.png 
gallery:
  - image_path: /assets/img/preserve.png
  - image_path: /assets/img/obstacle.png
  - image_path: /assets/img/GD.png
  - image_path: /assets/img/printedhead.png
  - image_path: /assets/img/head2.png
  - image_path: /assets/img/head5.png

---

# Overview of the Part and Application

* **The Head and its Adjustments:** This project enabled me to explore the applications of generative design by reducing the mass of a lacrosse stick head and enhancing its mechanical performance through functional lightweighting, resulting in an SLS (selective laser sintering) printed final model. I chose a lacrosse stick head for this project because I use a lacrosse stick almost every day here at Vanderbilt and know its intended functions and uses. After finding a simplified stick head model on GrabCad that looked like it could interchangeably function as a men's or women’s stick head, I decided to make the model even more of a hybrid by adding elements I think would be important for use in both sides of the game. The original model didn’t have stringing holes at the top of the stick so I made sure to add those for practical use. In addition, the head looked a bit bulkier than a traditional women’s stick head, so that was the main reason for wanting to lightweight the part. A component I felt would be beneficial for the stick’s use was to add a thin lining around the perimeter of the head’s pocket hole. There was two main reasons for incorporating this lining: 1) to provide an extra layer of support to the head’s structure for catching, throwing, and shooting lacrosse balls so that the newly lightweighted part would still maintain its strength and 2) the lining projects further than the back of the original head to help players dig into their opponent’s pocket on the faceoff and draw, as well as provide support for ground balls. In a real-world application/context, the goal would be for this generatively designed head to withstand the same use that a mass-manufactured stick head can withstand.  

# Preserve and Obstacle Geometry

* **Preserve Geometry:** The critical preserved regions in my model included the base of the head where the shaft of the stick inserts to, the added lining on the back of the stick for the faceoff/draw and ground balls, and the perimeter of the newly adding stringing holes at the top of the head. These components are crucial to the functionality of the head and needed to be included in the lightweight part. I also felt that preserving these components as preserved geometry helped give the generative design some guidance on how to proceed with lightweighting the rest of the model.
* **Obstacle Geometry:** Whereas other crucial sections needed to incorporate obstacle geometry, or space the generative design must avoid when generating the new model. The most important obstacle geometry was placed directly in the open space of the center of the head. This area is strictly designed to have lacrosse stringing or mesh to catch/throw/shoot the lacrosse ball, so I had to make sure the generative design wouldn’t even try to build in this area. I also placed an obstacle inside the base of the lacrosse head where the hypothetical lacrosse shaft would be, because if the generative design built part of the model in this area, then the stick wouldn’t fit together properly. In addition, I made symmetric obstacle geometries on the side walls of the stick head to guarantee there would be space for a mesh pocket to attach to. Lastly, I created obstacles within the holes at the top of the head to additionally make sure that the generative design didn’t try to build in these areas for a mesh pocket to be attached. 

# Load Case Application and Structural Constraints 

* **Gravity Load:** I used three different types of load cases in the design study to help give it the best understanding of how the part is intended to function and what loads it would need to bear. The first load is gravity, which seems implied, but is important in understanding what direction it's hitting the part at. I placed the gravity load to push directly down on the stick head as the stick head is vertically positioned in Fusion360. 
* **Direct Force Load:** I then applied direct force loads to simulate the loads that would be experienced on the stick head during a practice or game. The first was applied to the thin lining on the back of the head to simulate the force the head would have to withstand during catching, throwing, or shooting, as the pocket pulls on the head structure. The estimated peak force of any of these actions has the ball moving around 60-90mph, which helped determine the magnitude of the load.
The second was applied to the top region on the back side of the head, the bottom scoop edge, to simulate the pressure the head would endure when scooping up a ground ball from the grass or turf. This force had to be positioned opposite the motion vector, so as the bottom scoop edge makes contact with the ground, the force is being pushed up onto that bottom edge. With the momentum of the player running while simultaneously pushing the end of the stick head into the ground to scoop up the ball, I figured that a substantial amount of force was needed to emulate this load, but less than the load required from the catching/throwing/shooting actions. 
* **Direct Moment Load:** Lastly, I applied a direct moment load at the base of the stick head to represent the rotating motion that the head would have to endure while cradling the ball, as well as withstand checks from the opponent. This load has the least momentum compared to the other loads mentioned. 
If I wanted to test my real-world model to further refine the loads for greater accuracy, I could string up the stick head with a mesh or fully-strung pocket, place the head onto a lacrosse shaft, and go out onto the field to go through fundamentals of the sport to see if it withstands the forces that I think are notable, while also seeing which loads I might need to consider and apply. 
* **Structural Constraints:** As for the structural constraints, I really only applied them in two main areas of my model. I created a fixed constraint at the throat/base of the head, where the stick shaft and head come together, as they form a single unit when assembled and do not move independently of each other. I also placed constraints on the four stringing holes at the top of the stick to model light string tension. I didn’t want to add more constraints because if an object is over-constrained, it can disrupt the generatively designed model and cause it to produce unusual shapes or a heavier final product. 

# Critique of Generative Design 

* **My Model:** Generative design proved itself very useful to me during this project, as it streamlined the model in areas that I would not have identified otherwise. I can see how it is wildly beneficial for practical engineering or prototyping, allowing for the production of the most efficient and lightweight designs. The main limitation I encountered was the printed model’s brittle piece of lining on the bottom scoop edge. I had hoped that, because I made it clear that the lining was a preserved geometry and placed the force load on it to simulate a ground ball scenario, this area of the stick head would exhibit great strength in the model. Yet, this portion of the print ended up being flimsy, and one side broke off from the main model. 
* **Where GD is Useful and Where it Falls Short:** The industry where generative design would prove most useful is in the realm of aviation and aerospace, as well as architecture. As an architecture major, I look forward to continuing to utilize and deepen my understanding of generative design in the field. Firms can use generative design to explore and generate thousands of building layouts to help find the perfect in-between of structural constraints and client preferences. I feel like generative design would fall short in regard to human judgment. While it can produce impressive results and helpful outcomes, it cannot grasp aesthetics that a human designer or builder can. 

# CAD Model
<iframe src="https://vanderbilt643.autodesk360.com/g/shares/SH286ddQT78850c0d8a4168e4592a124b886?
mode=embed" width="640" height="480" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true"  frameborder="0"></iframe> 

# Table of the Forces Applied

| Name of Force | Magnitude | Location of Force Application | Short Rational |
| :-- | :-- | :-- | :-- | 
| Gravity | 9.807 m/s^2 | Entirety of Object | Standard for All Models
| Direct Force | 100.00 N | Bottom Scoop Edge | Ground Ball Impact 
| Direct Force | 150.296 N | Added Pocket Lining | Catching, Throwing, Shooting
| Direct Moment | 4.00 N m | Base/Neck of Object | Cradling, Getting Checked

{% include gallery caption="Preserved and Obstacle Geometries, Generative Design Iterations, Printed Stick Head" %}
