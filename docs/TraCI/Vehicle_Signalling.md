---
layout: post
title: TraCI Vehicle Signalling
permalink: /TraCI/Vehicle_Signalling/
---

A vehicle's signals are encoded in an integer, each by one bit, encoding whether the according signal/... is on or off. Most signals are rather meant to be used by an external application. The following signals are special:

-   “VEH_SIGNAL_BRAKELIGHT”: computed each time step, used by the vehicles when trying to avoid jamming on an intersection. The value set via TraCI is only retained for the current time step
-   “VEH_SIGNAL_BLINKER_RIGHT” and “VEH_SIGNAL_BLINKER_LEFT”: computed each time step, The value set via TraCI is only retained for the current time step
-   “VEH_SIGNAL_EMERGENCY_BLUE: when switched on, a blinking blue light is shown in the GUI for vehicles with vClass=”emergency" and shapeClass=“emergency”

The following table shows the defined signals.

|                                 |     |
|---------------------------------|-----|
| Name                            | Bit |
| VEH_SIGNAL_BLINKER_RIGHT     | 0   |
| VEH_SIGNAL_BLINKER_LEFT      | 1   |
| VEH_SIGNAL_BLINKER_EMERGENCY | 2   |
| VEH_SIGNAL_BRAKELIGHT         | 3   |
| VEH_SIGNAL_FRONTLIGHT         | 4   |
| VEH_SIGNAL_FOGLIGHT           | 5   |
| VEH_SIGNAL_HIGHBEAM           | 6   |
| VEH_SIGNAL_BACKDRIVE          | 7   |
| VEH_SIGNAL_WIPER              | 8   |
| VEH_SIGNAL_DOOR_OPEN_LEFT   | 9   |
| VEH_SIGNAL_DOOR_OPEN_RIGHT  | 10  |
| VEH_SIGNAL_EMERGENCY_BLUE    | 11  |
| VEH_SIGNAL_EMERGENCY_RED     | 12  |
| VEH_SIGNAL_EMERGENCY_YELLOW  | 13  |

**See also**:

-   [Vehicle Value Retrieval](/TraCI/Vehicle_Value_Retrieval "wikilink")
-   [Change Vehicle State](/TraCI/Change_Vehicle_State "wikilink")
-   [Accessing signal state without TraCI using ](/Simulation/Output/FCDOutput#Further_Options "wikilink")
