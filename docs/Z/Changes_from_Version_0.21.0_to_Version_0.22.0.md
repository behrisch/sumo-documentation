---
title: Z Changes from Version 0.21.0 to Version 0.22.0
permalink: /Z/Changes_from_Version_0.21.0_to_Version_0.22.0/
---

Version 0.22.0 (11.11.2014)
---------------------------

### Bugfixes

-   Simulation
    -   Vehicles with now properly adapt their speed to vehicles ahead at insertion. This results in higher flows.
    -   Teleporting vehicles will only be inserted if they fit fully onto the destination lane.
    -   Fixed some inconsistencies in E3-Detector output (see [E3 Further_Notes](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3)#Further_Notes "wikilink")).
    -   Flows using attribute now correctly terminate when attribute is given.
    -   Fixed several bugs for traffic lights of type .
    -   Pedestrians using the model now always respect attribute
    -   Fixed crash when computing pedestrians positions on short walkingAreas.
    -   Fixed crash when using car following model
    -   Fixed bug that was causing collisions at intersections.
    -   Fixed bug that was causing collisions due to unsafe lane-changing decisions.
    -   Fixed bug that was causing collisions due to unsafe insertion.
    -   Fixed bug that was causing collisions due to unsafe re-insertion after teleporting.
    -   Fixed bug that was causing *silent* collisions between vehicles on different edges. Previously this type of collision was not reported but visible in the gui.
    -   Fixed bug that sometimes lead to inferior lane-change decisions in networks with vehicle class restrictions.
    -   Fixed bugs that sometimes prevented vehicles from being inserted at the earliest opportunity.
    -   Fixed bug that prevented vehicles from being inserted when their was close to their and using car following model .
    -   Fixed bug that was causing unnecessary lane changes leading to oscillations.
    -   Fixed bug that was degrading the cooperation between vehicles during lane changing.
    -   Flows now always insert at least 1 vehicle for any positive repetition period (if the simulation time reaches the -time).
    -   Fixed position caching which caused wrong positions and angles after lane changes
    -   Fixed bluetooth reentry see
    -   Fixed the usage of different random number generators for route file parsing and vehicle movement
    -   Fixed rerouting close to junctions

<!-- -->

-   SUMO-GUI
    -   Single-stepping the simulation with hotkey (*Ctrl-D*) is now working as smoothly as intended.
    -   Changing simulation delay via mousewheel now works when the pointer is on top of the dial.
    -   Vehicle coloring *by acceleration*, *by time gap* and *by offset from best lane* now correctly visualize negative values
    -   Persons which are waiting or riding in a a vehicle now face the correct direction.
    -   Fixed crash related to parking vehicles.
    -   Corrected angle of parking vehicles.
    -   Fixed bug where train carriages were drawn incorrectly.
    -   The drawing size of laneAreaDetectors can now be scaled properly.

<!-- -->

-   NETCONVERT
    -   Street-sign-output now references the correct xsd file.
    -   warnings are emitted if no proj support is available and projection is needed

<!-- -->

-   DUAROUTER
    -   Fixed crash when using options and .
    -   Fixed crash when using option .
    -   When using option the non-looping parts of the route are now kept unchanged as intended.
    -   Progress indicator is now only shown if the option is used.
    -   Fixed crash when loading with attribute .

<!-- -->

-   TraCI
    -   Fixed crash when retrieving vehicle variable best lanes (id 0xb2) while the vehicle is on an internal lane.
    -   The command induction loop value ([last step vehicle data Command_0x17](/TraCI/Lane_Area_Detector_Value_Retrieval "wikilink"))) now returns the value **-1** for the *leaveTime* of a vehicle which has not yet left the detector (instead of returning the current time step as before).
    -   Fixing connection retries in the python client

<!-- -->

-   Misc
    -   Fixed includes to speed up compilation

### Enhancements

-   Simulation
    -   Whenever rerouting vehicles, a new route is only recorded when it differs from the previous route.
    -   tripinfo-output now includes attribute which holds the time loss compared to the maximum driving speed.
    -   Added option . When this is set, tripinfo output will additionally be written for all vehicles that did not arrive at the end of the simulation.
    -   Vehicles with the attribute now consider the free space on all candidate lanes instead of the number of vehicles. This results in higher flow.
    -   Added a new departLane-value named where vehicles are inserted on the rightmost lane they are allowed to use; this is the new default insertion lane
    -   Now supports parallel routing by using the option
    -   Added new routing algorithms 'astar' and 'CH' which are faster than the default 'dijkstra' algorithm.
    -   elements with attributes and can now be loaded directly in the simulation and will automatically be routed according to the current traveltimes at .

    -   Invalid stops now generate better error messages, see
    -   Added option . This allows to generate vehicle route files which reproduce the original behavior when using one shot routing.
    -   Added option to disturb edge weights when routing in the simulation. This allows modelling imperfect information, helps to avoid biases when multiple routes have the same length (i.e. in grid networks) and may be used to prevent jams on a single shortest path.

<!-- -->

-   SUMO-GUI
    -   Now appending *.xml* suffix when saving viewport, view settings or decals
    -   Added lane coloring *by loaded weights*. This colors by whatever attribute was set with option . The weight value is also shown in the parameter dialog.
    -   Added lane coloring *by priority*. This uses the edge priorities used during network creation. The priority value is also shown in the parameter dialog.
    -   Added junction coloring *by type*.
    -   Added visualization options for drawing vehicles, persons, POIs, polygons and additional gui objects with constant size when zooming out.
    -   The dialog for changing visualization settings is now resizable and will remember its size across application runs. All settings are now scrollable to allow work on smaller screens.
    -   The attributes which can be used to customize lane colors can now also be used to scale their width. This is done in the view customization dialog unter 'Streets' -&gt; 'Scale width'. See [1](http://sumo-sim.org/blog/wp-content/uploads/2014/08/scaling_by_speed-300x281.png).
    -   Vehicle coloring ''by time since lane change' now indicates the direction of the change by its color
    -   Added new link state 'u' to encode red-yellow phase (shown as orange). Vehicles behave as if 'r' (red) was set. This linkstate may be used to indicates upcoming green phase according to [RiLSA](http://de.wikipedia.org/wiki/Richtlinien_f%C3%BCr_Lichtsignalanlagen).
    -   Lane coloring by speed now uses more colors (the same as vehicle coloring by speed).
-   NETCONVERT
    -   Roundabouts can now be specified via [plain-xml input](/Networks/Building_Networks_from_own_XML-descriptions#Roundabouts "wikilink"). They are also written to the *.edg.xml*-file when using option .
-   DUAROUTER
    -   Now supports parallel routing by using the option
    -   Added new routing algorithms 'astar' and 'CH' which are faster than the default 'dijkstra' algorithm.
-   JTRROUTER
    -   Routes which loop back on themselves are no longer genereated by default (can be enabled using option ).

<!-- -->

-   TraCI
    -   added method *vehicle.setSpeedMode()* to the python API ([command 0x3b](/TraCI/Change_Vehicle_State "wikilink"))).
    -   added method *areal.getLastVehicleIDs()* to the python API ([Command_0x12](/TraCI/Lane_Area_Detector_Value_Retrieval "wikilink"))).
    -   added argument *extended* to method *lane.getLinks()* in the python API (default *False*). If it is set to *True*, the method returns all the information defined for ([Command_0x33](/TraCI/Lane_Value_Retrieval "wikilink"))) instead of a subset.

<!-- -->

-   Tools
    -   Added [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") option to generate weight files which can be used to visualize the edge probabilities for being source/destination/via in [SUMO-GUI](/SUMO-GUI "wikilink").
    -   Added [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") option which allows loading edge probabilities for being source/destination/via. The file format is the same as for option with missing edges defaulting to probability 0 and missing files defaulting to normal randomization.
    -   Added [dua-iterate.py](/Tools/Assign#dua-iterate.py "wikilink") option to zip old iteration outputs using 7-zip
    -   Added script [server.py](/Tools/Import/OSM#server.py "wikilink") for “three-click” scenario generation (thanks to Jakob Stigloher)
-   [MAROUTER](/MAROUTER "wikilink")
    -   Added new router which reads trips and writes routes by computing a macroscopic user assignment.

### Other

-   Web presence moved to sumo.dlr.de (wiki at sumo.dlr.de/wiki, trac at sumo.dlr.de/trac)

<!-- -->

-   Documentation
    -   Added [description of generic NETCONVERT warnings](/NETCONVERT#Warnings_during_Import "wikilink").
    -   Added [description of OSM-specific NETCONVERT warnings](/Networks/Import/OpenStreetMap#Warnings_during_Import "wikilink").
    -   Added [description of Windows build configurations](/Installing/Windows_Build#Available_Builds "wikilink").

<!-- -->

-   DUAROUTER
    -   Now issuing warnings about repaired routes.

<!-- -->

-   SUMO-GUI
    -   Tweaked right-of-way colors for types *stop* and *allway_stop*. [All colors are now documented.](/SUMO-GUI#Right_of_way "wikilink")

<!-- -->

-   Misc
    -   The version string for each application now includes the flag 'D' for the debug-build and flag 'I' for the internal build
    -   The traceExporter.py script moved from /tools/bin to /tools
    -   unittest compilation is automatically enabled when gtest is found (Linux only)
