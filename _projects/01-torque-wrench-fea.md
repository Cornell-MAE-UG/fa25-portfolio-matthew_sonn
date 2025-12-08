---
layout: project
markdown: 1
title: Torque Wrench Design & FEM
description: Designing a torque wrench based on a FEM
technologies: [Autodesk Fusion, MATLAB, ANSYS]
image: /assets/images/Screenshot 2025-12-07 215932.png
---


![torquewrenchsetup]({{ "assets/images/Screenshot 2025-12-07 224150.png" | relative_url }}){: .inline-image-l style="width: 400px"}

My final project for MAE 3270: Mechanics of Engineering Materials was to design a torque wrench's dimensions and choose a material such that it meets the following requirements:

- Attain at least 1.0 mV/V output at the rated torque of 600 in-lbf
- Safety factor of X=4 for yield or brittle failure
- Safety factor of X=2 for crack growth from an assumed crack of depth 0.04 inches (1 mm)
- Fatigue stress safety factor of X = 1.5
- Material must bee a steel, aluminum, or titanium alloy

A baseline design was provided, and I worked in a group to write a script that we could use to iterate on the baseline design to create a better design. More details on the baseline design and Finite Element Analysis performed on the baseline design can be found in the preliminary report here assets/MAE 3270 Final Project Part I.pdf. Using the script and the Granta software, we found a material and iterated through dimensions to find a combination that met all of the requirements. 
