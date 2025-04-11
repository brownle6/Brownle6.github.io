---
title: "Top-Down Modeled Bike Phone Holder"
excerpt: "Filament-Printed Bike Phone Holder with Rotating Detent Mechanism"
header:
  image: /assets/img/bikeholderrendering2.png  
teaser: /assets/img/bikeholderrendering2.png 
gallery:
  - image_path: /assets/img/mountedonbike.png
  - image_path: /assets/img/sideview.png
  - image_path: /assets/img/detent.png
  - image_path: /assets/img/lid.png
  - image_path: /assets/img/sidedetent.png
  - image_path: /assets/img/phoneholder.GIF
  - image_path: /assets/img/sideanalysis.png
  - image_path: /assets/img/detentanalysis.png
---

# Description

* **What are Print-in-Place Parts?** “Print-in-place models are functional, multiple-component designs that work immediately after removal from the print bed, and no post-processing or assembly is required. These can be created through single material extrusion by carefully designing models and orienting the print to allow for clearance between printed joints where motion or rotation is needed. However, even with optimized print settings, these models can be plagued by crunchy movement due to irregularities of plastic extrusion. Another method to obtain useful motion is to include a flexible element in the model, whether that is a thin piece of rigid plastic or a second elastomeric material” (Florian, 2025). Pros about print-in-place parts is that they’re typically more functional parts due to the different rigidities of plastics used and they can be multi-colored. A common application for print-in-place includes needle nose pliers, which is the project you will read about shortly. Specifically, our pliers had to be capable of gripping and picking up through-hole resistors and use a flexible material for the spring component that returns them to their open position when not in use. Other applications where print-in-place has been used is for 3D printable print-in-place gear bearings. 3D printing typically struggles with printing a standard ball bearing, so this print-in-place printable gear replaces balls with gears that lock together because FDM 3D printers typically aren’t great at printing spheres, and adding outside pieces, like metal balls, adds to the overall construction time. In addition, print-in-place can also make sliding bolt locks. This piece can be printed entirely at once, but if preferred, can be printed with individual parts to have spheres available (Garbett, 2022). Popular material combinations for print-in-place include PLA (rigid) and TPU (elastic), PLA and PVA with water soluble supports, ABS and HIPs, as well as fresh and recycled material. For the pliers project, I used PLA and TPU together to provide me with the needed strength and flexibility for maximum efficiency. 

# About the Design and Iterative Process

* **The spring component in the pliers is made from the central piece of the pliers, which was made with TPU, an elastic material that allows for flexibility within the model. In order for this middle piece to be flexible, a rectilinear grid using Superslicer was implemented at an angle for shear behavior to allow the pliers to return to their original position. If this middle piece was made with PLA, a rigid plastic, there would be no shear behavior because the material is too stiff to bend in any direction without breaking. For the PLA components of the pliers to fit snugly into the TPU central piece, I used form fitting dovetail joints in my CAD model. In order to print these pieces, I used a multi-material single extrude printer where I printed all the PLA pieces first, then printed the TPU piece separately. The jaws of my pliers were approximately 33mm long, and because of the slender and lightweight design of the pliers, its jaw capacity was fairly light. Fortunately, I only had to print my pliers once, and they turned out to be successful without having to reprint.**

# CAD Model
 <iframe src="https://a360.co/4jxKM1v
=embed" width="640" height="480" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true"  frameborder="0"></iframe>

{% include gallery caption="Pliers with CAD Renderings" %}

# Works Cited
Garbett, Samuel L. “Learn Print-in-Place 3D Printing with These 7 Projects.” MUO, Valnet, 8 Sept. 2022, www.makeuseof.com/print-in-place-3d-printer-projects/. 
