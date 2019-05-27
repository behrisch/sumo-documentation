---
title: Simulation Emergency
permalink: /Simulation/Emergency/
---

Emergency Vehicle simulation
============================

The simulation of emergency vehicles and their special rights is partially possible with SUMO. Additional capabilities are planned for the future.

-   Disregarding right-of-way and traffic lights: This is supported by using the [TraCI 'speed mode' command](/TraCI/Change_Vehicle_State#speed_mode_.280xb3.29 "wikilink") to disable intersection related safety checks.
-   Exceeding the speed limit: This is supported by setting the vType-attribute [*speedFactor*](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") (a value of 1.5 allows driving with 150% of the road speed limit).
-   Driving in a virtual middle lane on a multi-lane road: This is supported by using the [sublane model](/Simulation/SublaneModel "wikilink"). The cooperative behavior of the surrounding traffic is not automatic and must be forced via TraCI commands.
-   Overtaking on the right: This is always permitted for vehicles with

Visualization
=============

The visualization of emergency vehicles is supported in [SUMO-GUI](/SUMO-GUI "wikilink"). When setting the vType-attribute a white vehicle with the international sign for first aid is drawn. Furthermore a police car will be drawn with vType-attribute and a firebrigade with vType-attribute . When additionally setting the vType-attribute a blue flashing light will be drawn also.

[<File:Ev.png>](/File:Ev.png "wikilink")

References
==========

Bieker, Laura (2015) Traffic safety evaluations for Emgergency Vehicles. Young Researchers Seminar, 17.-19. Juni 2015, Rom, Italien.

Bieker, Laura (2011) Emergency Vehicle Prioritization using Vehicle-To-Vehicle Communication. Young Researchers Seminar, 8.-10. Jun. 2011, Kopenhagen, Dänemark.