---
layout: project
title: Laser Construction
description: Built a Nitrogen Laser
technologies: [Soldering, Circuit Analysis, Circuit Organization]
image: /assets/images/laser-pic.jpg
---

<video src="{{ 'assets/laser-operation.MP4' | relative_url }}" controls muted preload="none" style="width: 400px; border-radius: 10px;"></video>

[NITROGEN LASER REPORT]({{ "assets/AEP 1110 Construction Lab Report.pdf" | relative_url }}).

For this project I helped build and test a nitrogen laser system made up of a pulse generator, the pulse amplifier circuit I constructed, and a chassis unit that holds the laser tube and high voltage discharge hardware. We wired these subsystems so that the low voltage pulse generator triggers the pulse amplifier, which in turn delivers a fast, high voltage pulse to the chassis to create a discharge in nitrogen gas and produce laser light. As part of this work I learned the basic physics behind lasers, including spontaneous and stimulated emission, population inversion in nitrogen, and why a short, intense electric pulse is needed to drive the gas into a lasing state. A video of the laser operating is included in my portfolio, and it is intentionally dark so the laser beam and glow from the discharge are clearly visible.

The Pulse Generator Circuit is shown below:

![Damper Springs]({{ "assets/images/Screenshot 2025-11-05 224114.png" | relative_url }}){: .inline-image-l style="width: 400px"}

My main technical responsibility was constructing and explaining the pulse amplifier circuit. This stage takes an 18 V control pulse from the pulse generator and uses a silicon controlled rectifier, capacitors, diodes, and a transformer to produce a sharp pulse of about 1600 V that drives the chassis. I used soldering, careful circuit organization, and circuit analysis skills to assemble the amplifier safely and to trace how charge moves through the capacitors and switching elements during each part of the pulse. After construction I presented the amplifier to my classmates and professor, walking through how the trigger signal at the SCR gate turns the high voltage path on and off and how the circuit resets between pulses so it is ready for the next shot.

The Pulse Amplifier Circuit (my contribution) is shown below:

![Damper Springs]({{ "assets/images/Screenshot 2025-11-05 223328.png" | relative_url }}){: .inline-image-l style="width: 400px"}

Once the laser was functioning we used it to run several experiments that connected the electronics to measurable physical effects. We measured how the photodiode signal, which tracks light intensity, depends on the high voltage power supply and identified the lasing threshold where stimulated emission starts to dominate. We then varied nitrogen pressure and saw how low and high pressures both reduce output by changing the mean free path of electrons, and finally we used two photodiodes at different distances from the laser to obtain an experimental value for the speed of light from the slope of distance versus time data. Working through these measurements reinforced both the underlying laser physics and the importance of clean circuit design and organization, since any timing or amplitude issues in the pulse amplifier would have shown up directly in the laser output and the data we collected.

As a part of this class, I also analyzed the features of a Carbon Dioxide Laser and culminated my findings in a report [here]({{ "assets/Carbon Dioxide Laser Lab Report.pdf" | relative_url }}).
