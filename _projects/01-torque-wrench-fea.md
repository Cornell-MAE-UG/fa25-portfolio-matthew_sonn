---
layout: project
markdown: 1
title: Torque Wrench Design & FEM
description: Designing a torque wrench based on a FEM
technologies: [Autodesk Fusion, MATLAB, ANSYS]
image: /assets/images/Screenshot 2025-12-07 215932.png
---


![torquewrenchsetup]({{ "assets/images/Screenshot 2025-12-07 224150.png" | relative_url }}){: .inline-image-r style="width: 400px"}

My final project for MAE 3270: Mechanics of Engineering Materials was to design a torque wrench's dimensions and choose a material such that it meets the following requirements:

- Attain at least 1.0 mV/V output at the rated torque of 600 in-lbf
- Safety factor of X=4 for yield or brittle failure
- Safety factor of X=2 for crack growth from an assumed crack of depth 0.04 inches (1 mm)
- Fatigue stress safety factor of X = 1.5
- Material must bee a steel, aluminum, or titanium alloy

A baseline design was provided, and I worked in a group to write a script that we could use to iterate on the baseline design to create a better design. More details on the baseline design and Finite Element Analysis performed on the baseline design can be found in the preliminary report [here]({{ "assets/MAE 3270 Final Project Part I.pdf" | relative_url }}). Using the script and the Granta software, we found a material and iterated through dimensions to find a combination that met all of the requirements:

**Material:** Carbon Steel, AISI 1080, oil quenched & tempered at 315 degrees Celsius

**Dimensions:** L = 16 in; h = 0.52 in; b = 0.45 in; c = 0.25 in

**Results:** load point deflection = 0.3348 in; max normal stress = 29.6 ksi; safety factor for strength = 4.3264; safety factor for crack growth = 2.0943; safety factor for fatigue = 2.3390; strain at gauge = 0.0010; strain gauge output = 1.0043 mV/V

The Torque Wrench with the improved design geometry was rendered in Fusion 360, then imported to ANSYS. An image of the Fusion Model labeled with the relevant dimensions is below:

![torquewrenchsetup]({{ "assets/images/Screenshot 2025-12-07 231013.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The material chosen is Carbon steel, AISI 1080, oil quenched & tempered at 315 degrees Celsius. AISI 1080 is a high-carbon steel (≈0.80% C) known for developing very high hardness and strength after heat treatment. When oil-quenched from the austensizing temperature and tempered at 315 °C, the microstructure becomes tempered martensite, providing a balance of tensile strength, high yield strength, and good elastic modulus retention. Tempering at this intermediate temperature reduces brittleness while preserving the high hardness needed for resisting wear and maintaining dimensional stability under repeated loading.

The CAD model was then imported into ANSYS, and boundary conditions were applied. The drive is 0.5" tall, but clamped boundary conditions were only applied to the upper 0.4" of the drive, leaving the 0.1" below it free. A force of 37.5 lbf, which equates to a moment of 600 in-lbf was applied to the end of the rod, a distance L from the center of the drive (L=16").

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.3-final.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The model was run with the applied boundary conditions and the updated geometry. The normal strain contours in the strain gauge direction (z) are below:

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.4-normalstraincontours.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The contour plot of maximum principal stresses from the FEM are below:

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.5-maxprincipalstresses-anotherview.png" | relative_url }}){: .inline-image-c style="width: 600px"}

Maximum Normal Stress from the FEM (contours below): 68.1 ksi

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.6-maxnormalstress.png" | relative_url }}){: .inline-image-c style="width: 600px"}

