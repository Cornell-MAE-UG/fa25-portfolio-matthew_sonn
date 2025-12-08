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

A baseline design was provided, and I worked in a group to write a script (see below) that we could use to iterate on the baseline design to create a better design. More details on the baseline design and Finite Element Analysis performed on the baseline design can be found in the preliminary report [here]({{ "assets/MAE 3270 Final Project Part I.pdf" | relative_url }}). 

```matlab
M = 600; % max torque (in-lbf)
L = 16; % length from drive to where load applied (inches)
h = 0.75; % width
b = 0.5; % thickness
c = 1.0; % distance from center of drive to center of strain gauge
E = 32.E6; % Young's modulus (psi)
nu = 0.29; % Poisson's ratio
su = 370.E3; % tensile strength use yield or ultimate depending on material (psi)
KIC = 15.E3; % fracture toughness (psi sqrt(in))
sfatigue = 115.e3; % fatigue strength from Granta for 10^6 cycles
name = 'M42 Steel'; % material name
% Find Load Point Deflection and Max Normal Stress:
F = M/L;
r = h/2;
I = (b*h^3)/12;
loadpointdeflection = (M*L^2)/(3*E*I)
maxnormalstress = M*r/I
% Find Safety Factors:
a = 0.04;
x = a/h;
Y = 1.12;
Kmax = Y*maxnormalstress*sqrt(pi*a);
sf_strength = su/maxnormalstress
sf_crackgrowth = KIC/Kmax
sf_fatigue = sfatigue/maxnormalstress
%Find Strain Gauge Results:
bendingstress = F*(L-c)*r/I;
strainatgauge = bendingstress/E
output = strainatgauge*1e3 %mV/V
```


Using the script and the Granta software, we found a material and iterated through dimensions to find a combination that met all of the requirements:

**Material:** Carbon Steel, AISI 1080, oil quenched & tempered at 315 degrees Celsius

**Dimensions:** L = 16 in; h = 0.52 in; b = 0.45 in; c = 0.25 in

**Results that Meet the Design Requirements:** load point deflection = 0.3348 in; max normal stress = 29.6 ksi; safety factor for strength = 4.3264; safety factor for crack growth = 2.0943; safety factor for fatigue = 2.3390; strain at gauge = 0.0010; strain gauge output = 1.0043 mV/V

The Torque Wrench with the improved design geometry was rendered in Fusion 360, then imported to ANSYS. An image of the Fusion Model labeled with the relevant dimensions is below:

![torquewrenchsetup]({{ "assets/images/Screenshot 2025-12-07 231013.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The material chosen is Carbon steel, AISI 1080, oil quenched & tempered at 315 degrees Celsius. AISI 1080 is a high-carbon steel (≈0.80% C) known for developing very high hardness and strength after heat treatment. When oil-quenched from the austensizing temperature and tempered at 315 °C, the microstructure becomes tempered martensite, providing a balance of tensile strength, high yield strength, and good elastic modulus retention. Tempering at this intermediate temperature reduces brittleness while preserving the high hardness needed for resisting wear and maintaining dimensional stability under repeated loading.

The CAD model was then imported into ANSYS, and boundary conditions were applied. The drive is 0.5" tall, but clamped boundary conditions were only applied to the upper 0.4" of the drive (light green shaded section in the image below), leaving the 0.1" below it free. A force of 37.5 lbf, which equates to a moment of 600 in-lbf was applied to the end of the rod, a distance L from the center of the drive (L=16").

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.3-final.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The model was run with the applied boundary conditions and the updated geometry. The normal strain contours in the strain gauge direction (z) are below:

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.4-normalstraincontours.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The contour plot of maximum principal stresses from the FEM are below:

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.5-maxprincipalstresses-anotherview.png" | relative_url }}){: .inline-image-c style="width: 600px"}

Maximum Normal Stress from the FEM (contours below): 68.1 ksi

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.6-maxnormalstress.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The deflection of the load point from the FEM (contours below): 0.38314 in

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.6-deflection.png" | relative_url }}){: .inline-image-c style="width: 600px"}

The strain at the strain gauge location (c = 0.25 in) was also determined by the FEM which is shown below: 930 microstrain

![torquewrenchsetup]({{ "assets/images/MAE3270-5.2.1.6-strainatgauge.png" | relative_url }}){: .inline-image-c style="width: 600px"}

From this strain, the torque wrench sensitivity in mV/V measured from the FEM is around 0.930 mV/V. Although the hand calculations give a value that meets the sensitivity requirement of 1 mV/V, the FEM produces a slightly lower value. In order to be safe, we can select a full-bridge strain gauge that will double our sensitivity: The maximum principal strain available for measurement at the intended probe location is approximately 930 microstrain. This strain value corresponds to the applied torque used in the ANSYS simulation and therefore represents the full-scale operating strain for the sensor installation. A foil strain gauge bonded at this location produces an electrical output proportional to strain through the gauge factor, GF. For small strains, the bridge output of a Wheatstone bridge can be approximated with the following standard relationships:

- Quarter-bridge output: DeltaV/V = (GF * epsilon) / 4
- Half-bridge output: DeltaV/V = (GF * epsilon) / 2
- Full-bridge output: DeltaV/V = GF * epsilon

Using a typical gauge factor of 2.1 and the FEM strain epsilon = 930 microstrain, the predicted full-scale electrical outputs are:

- Quarter-bridge: .488 mV/V
- Half-bridge: .976 mV/V
- Full-bridge: 1.95 mV/V

These values represent the torque-wrench sensitivity for the torque level applied in the FEM (600 in-lbf).

**Strain Gauge Selection:** 

![torquewrenchsetup]({{ "assets/images/Screenshot 2025-12-07 235451.png" | relative_url }}){: .inline-image-r style="width: 400px"}
Four matched 350-ohm constantan linear foil gauges (e.g., Micro-Measurements CEA-series), .01 in gauge length, arranged in a full-bridge bending configuration with a GF of 2.11 +- 1.0%. The strain gauge selection was based on the available mounting width of less than 0.45 in (.31 in) and the need to measure the principal bending strain identified in the FEM. A linear foil gauge was required to align with the dominant strain direction, and a gauge length between 0.125 and 0.25 in was chosen to provide adequate strain averaging while keeping the backing width (~0.20 in) within the geometric limit. A 350-ohm constantan foil gauge was selected to minimize self-heating and ensure stable output. A full-bridge configuration would ideally be chosen to maximize sensitivity, improve temperature compensation, and provide a balanced bending-strain measurement suitable for torque wrench calibration.
