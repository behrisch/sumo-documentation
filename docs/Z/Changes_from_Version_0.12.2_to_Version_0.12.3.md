---
title: Z Changes from Version 0.12.2 to Version 0.12.3
permalink: /Z/Changes_from_Version_0.12.2_to_Version_0.12.3/
---

**Release Date: 10.02.2011**

-   all
    -   License update to GPL v3+
    -   verbose “--version” option concerning license
    -   fixing a lot of compiler warnings
-   dfrouter
    -   generate plain vehicles instead of emitters
-   duarouter
    -   c-Logit Model implementation
-   Simulation
    -   tweaks to gap computation to avoid collisions
    -   Added two further departpos-values, “<span class="inlxml">pwagSimple</span>” and “<span class="inlxml">pwagGeneric</span>” which try to achieve a higher flow. See: [Definition_of_Vehicles,_Vehicle_Types,_and_Routes\#departpos](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#departpos "wikilink")
    -   removing person-related deadlocks
    -   improving vehicle routes output
-   TraCI
    -   please note that the encoding of a vehicle's angle has changed, see [Vehicle_Values\#Angle](/Vehicle_Values#Angle "wikilink")
-   SUMO-GUI
    -   corrected vehicle's angle (was [ticket\#430](http://sourceforge.net/apps/trac/sumo/ticket/430))
    -   Clipboard works under Linux
