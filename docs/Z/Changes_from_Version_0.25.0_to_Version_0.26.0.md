---
title: Z Changes from Version 0.25.0 to Version 0.26.0
permalink: /Z/Changes_from_Version_0.25.0_to_Version_0.26.0/
---

Version 0.26.0 (19.04.2016)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed crash when rerouting a large number of vehicles in parallel. ,
    -   Fixes related to [*zipper* nodes](/Networks/Building_Networks_from_own_XML-descriptions#Node_types "wikilink").
        -   Fixed deadlock
        -   Fixed collision
        -   Fixed undesired non-determinism.
    -   Fixed collision of a vehicle with itself when departing at an edge that forms a tight circle.
    -   Fixed bug that was causing wrong vehicle counts in [summary output](/Simulation/Output/Summary "wikilink") and was preventing the simulation from terminating automatically when [continuing from a loaded state](/Simulation/SaveAndLoad "wikilink").
    -   Fixed route errors and crashing when [continuing from a loaded state](/Simulation/SaveAndLoad "wikilink") and using [routing devices](/Demand/Automatic_Routing "wikilink").
    -   Fixed bug that was causing false positives when calling *traci.inductionloop.getLastStepVehicleIds* and *traci.inductionloop.getLastStepVehicleNumber*.
    -   [Induction loop detectors](/Simulation/Output/Induction_Loops_Detectors_(E1) "wikilink") now count vehicles which occupy the detector position during insertion.
    -   Fixed collisions when using using continuous lane-changing.
    -   Fixed bug that was causing erratic emission behavior for stopped vehicles when using the [PHEMlight emission model](/Models/Emissions/PHEMlight "wikilink").
    -   Fixed unsafe traffic light plans when building networks without exclusive left-green phase.
    -   When using the [*striping* model](/Simulation/Pedestrians#Model_striping "wikilink"), pedestrians now avoid moving with near-zero speed.
    -   Fixed pedestrian collisions.
    -   Intersections with more than 64 connections can now be loaded.
    -   When approaching a [double-connection](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink") vehicles now prefer the lane with the prioritized connection.
    -   Fixed collision at [double-connection](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink").
    -   The default vehicle class is now when using the default vehicle type *DEFAULT_VEHTYPE*.
    -   Fixed stuck vehicles when teleporting past an closed edge with a [rerouter](/Simulation/Rerouter "wikilink").
    -   Fixed invalid route lengths in [tripinfo-output](/Simulation/Output/TripInfo "wikilink").
    -   [Rerouters](/Simulation/Rerouter "wikilink") rerouters that combine and now only apply to vehicles that are affected by the closed edges.
    -   [Rerouting devices](/Demand/Automatic_Routing "wikilink") can now be specified with [generic parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Devices "wikilink").
    -   Fixed invalid waiting position of pedestrians after walking.
    -   Fixed detector data for teleporting vehicles.
    -   Fixed meandata for circular networks.

<!-- -->

-   SUMO-GUI
    -   Fixed bug that was causing slightly exaggerated exit times to be shown when activating *Show Link Items* from the vehicle context menu.
    -   Fixed flickering brake lights due to small random decelerations.
    -   [Areal detectors](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink") can now be hidden by setting their size exaggeration to 0.
    -   Fixed invalid occupancy value for [lane area detectors](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink") (was exaggerated by a factor of 100).
    -   Fixed crashing related to showing and tracking parameters of arrived vehicles. ,
    -   Fixed glitch when drawing rail carriages on edges with customized length.
    -   Fixed coordinate update without mouse movement.
    -   Fixed time display switch in initial view.
    -   Vehicle shape and size are now correctly updated when set via TraCI.

<!-- -->

-   MESO
    -   Fixed bug that broke behavior (regression in 0.25.0).
    -   vClass-specific speed limits are now used.
    -   tripinfo-output now contains valid *timeLoss* values.
    -   Fixed invalid travel time computation during simulation routing (was averaging segments instead of vehicles).

<!-- -->

-   MESO-GUI
    -   Fixed crash.
    -   Coloring vehicles *by selection* is now working.

<!-- -->

-   NETEDIT
    -   Fixed bug that made it impossible to modify numerical attributes (lane numbers, phase duration etc.) on some computers.
    -   Fixed error when modifying signal plans for joined traffic lights.
    -   Fixed invalid edge length attribute when inspecting networks without internal links.
    -   Fixed bug where junctions with uncommon shapes could not be selected.

<!-- -->

-   NETCONVERT
    -   Fixed bug that was causing unsafe [internal junctions](/Simulation/Intersections#Waiting_Within_the_Intersection "wikilink") to be built. ,
    -   Fixed bug that was causing z-information to become corrupted. Thanks to Mirco Sturari for the patch.
    -   Fixed bug where pedestrians never got the green light when loading a *.net.xml* file and adding pedestrian crossings.
    -   Fixed bug where pedestrian *walkingarea* edges were missing. (This could cause invalid routes to be generated).
    -   Multiple connections from the same edge to the same target lane can now be set in post-processing (i.e. after removal of geometry-like nodes).
    -   Option now respects option .
    -   Fixed invalid traffic light plans for networks with pedestrian crossings.
    -   Loading [custom traffic light plans](/Networks/Building_Networks_from_own_XML-descriptions#Traffic_Light_Program_Definition "wikilink") now correctly affects the [building of internal junctions](/Simulation/Intersections#Waiting_Within_the_Intersection "wikilink").
    -   Several fixes in regard to OpenDrive networks:
        -   Added missing attribute when writing [OpenDrive](/Networks/Export#OpenDRIVE "wikilink") networks.
        -   Fixed geometry of lanes within intersections when writing [OpenDrive](/Networks/Export#OpenDRIVE "wikilink") networks.
        -   Fixed geometry of lanes when importing imprecise [OpenDrive](/Networks/Export#OpenDRIVE "wikilink") networks .
    -   Option now writes [xsd-conforming](/XMLValidation "wikilink") output.
    -   Fixed bugs that were causing invalid TLS plans to be generated for joined traffic lights. ,
    -   Fixed crash when importing OSM networks related to self-looping edges.
    -   Fixed bug that was causing invalid junction shapes and extremely large network boundaries.
    -   Fixed crashing (on Windows) and invalid traffic lights (Linux) when loading a *.net.xml* file and adding splits.
    -   Fixed invalid connections at edges with vClass-exclusive lanes. ,
    -   Fixed invalid traffic light plans for node type .
    -   Fixed unsafe junction logic when using custom tls plans with node type .
    -   Connections from lanes that are added during ramp guessing can now be specified.
    -   User-defined connections are no longer discarded at guessed ramps.
    -   Fixed error when guessing overlapping off-ramps.
    -   Fixed error when computing edge shapes with unusual input geometries.

<!-- -->

-   TraCI
    -   Multiple fixes to the [C++ TraCI library](/TraCI/C%2B%2BTraCIAPI "wikilink")
        -   commands *gui.setScheme, gui.getScheme*, *inductionloop.getVehicleData*
        -   various *set*-commands were not consuming all result bytes and thus corrupted the message stream. Thanks to Alexander Weidinger for the patch.
    -   Fixes to TraaS functions *Simulation_getDistance2D* and *Simulation_getDistanceRoad*.
    -   Fixed crash when using vehicle command *move to VTD*.
    -   vehicle command *move to VTD* can now position vehicles on internal lanes.
    -   Commands that return the road distance no longer return an exaggerated value in networks without internal links (distances across intersections were counted twice).
    -   vehicle command *distance* now takes the depart position into account (was using 0 before).

<!-- -->

-   Tools
    -   Fixed error that prevented [Tools/Visualization\#plot_net_dump.py](/Tools/Visualization#plot_net_dump.py "wikilink") from running.
    -   Fixed import errors in [vehrouteDiff.py](/Tools/Output#vehrouteDiff.py "wikilink") (formerly undocumented tool).
    -   [netdiff.py](/Tools/Net#netdiff.py "wikilink") now correctly handles non-ascii characters (i.e. international street names).
    -   [netdiff.py](/Tools/Net#netdiff.py "wikilink") now handles pedestrian crossings.

### Enhancements

-   Simulation
    -   [MESO](/MESO "wikilink") and [MESO\#MESO-GUI](/MESO#MESO-GUI "wikilink") are now open.
    -   Can now simulated rail road crossings (see NETCONVERT enhancement below). Vehicles will get a red light whenever a train is approaching.
    -   Added option for configuring the numerical precision of vehicle emissions.
    -   Added new [departPos](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#departPos "wikilink") value which can be used to maximize flow and still maintain vehicle ordering.
    -   [Rerouters](/Simulation/Rerouter "wikilink") now apply to vehicles that are already on the rerouter edge at the start of the active interval.
    -   Vehicles that are equipped with a [rerouting device](/Demand/Automatic_Routing "wikilink") now incorporate knowledge about the current traffic state when computing a new route due to encountering a [rerouter object](/Simulation/Rerouter#Assigning_a_new_Destination "wikilink").
    -   [Parking](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink") vehicles are no included in the [FCD-Output](/Simulation/Output/FCDOutput "wikilink").
    -   Riding [persons](/Specification/Persons#Rides "wikilink") and [containers](/Specification/Containers#Transports "wikilink") are now included in [FCD-Output](/Simulation/Output/FCDOutput "wikilink") and [Netstate-Output](/Simulation/Output/RawDump "wikilink"). ,
    -   The [car following model](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Car-Following_Models "wikilink") can now be defined using the new -attribute [carFollowModel](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") (as alternative to using a child XML-element).
    -   Added new [PHEMlight](/Models/Emissions/PHEMlight "wikilink") version.

<!-- -->

-   SUMO-GUI
    -   Adjusted zooming distance when centering on simulation objects to make objects easier to find.
    -   Added option for tracking accumulated waiting time of vehicles. The accumulated waiting time (seconds of waiting time within the configured interval, default 100s) can be inspected in the vehicle's parameter window and the vehicles can be colored according to this value.
    -   Lanes can now be colored *by routing device assumed speed*. This is an exponential moving average of mean travel speeds used for [dynamic rerouting](/Demand/Automatic_Routing "wikilink").

<!-- -->

-   MESO
    -   Added option as an alternative way to model the delay effects of traffic lights. When this option is set to a positive value, the expected delay time for each controlled link (based on red duration and cycle duration) is added to the travel time, multiplied with the argument. By calibrating the parameter, the quality of TLS coordination can be modeled.

<!-- -->

-   MESO-GUI
    -   Coloring vehicles *by depart delay* is now working. Added *depart delay* to the vehicle parameter dialog.
    -   Added *event time*, *entry time* and *block time* to the vehicle parameter dialog. These values record when a vehicle leaves, entered and was blocked on an edge segment.

<!-- -->

-   NETCONVERT
    -   Added new [node type *rail_crossing*](/Networks/Building_Networks_from_own_XML-descriptions#Node_types "wikilink") to model behavior at a rail road crossings.

<!-- -->

-   POLYCONVERT
    -   Added default typemaps similar to netconvert.

<!-- -->

-   DUAROUTER
    -   Added person trips and [IntermodalRouting](/IntermodalRouting "wikilink")
    -   When a flow has a stop definition with attribute , the time is shifted for each successive vehicle in the flow.

<!-- -->

-   MAROUTER
    -   Added bulk routing and better OD cell handling for speed improvements.

<!-- -->

-   TraCI
    -   The [python client](/TraCI/Interfacing_TraCI_from_Python "wikilink") is now thread safe when using multiple connections in parallel. Each opened connection returns an independent TraCI instance.
    -   Added support for vehicle commands to the [C++ TraCI library](/TraCI/C%2B%2BTraCIAPI "wikilink") Thanks to Alexander Weidinger for the patch.
    -   Added new [TraaS commands](/TraCI#Interfaces_by_Programming_Language "wikilink") *Edge.getLastStepPersonIDs, Person.getNextEdge, Vehicle.getRouteIndex, Vehicle.getStopState, Vehicle.isStopped* and some more stop-related vehicle commands.
    -   The angle argument of vehicle command [*move to VTD*](/TraCI/Change_Vehicle_State#Command_0xc4:_Change_Vehicle_State "wikilink") now overrides the vehicle angle for drawing and [fcd-output](/Simulation/Output/FCDOutput "wikilink").
    -   Added new simulation command [*save state 0x95*](/TraCI/Change_Simulation_State#Command_0xcc:_Change_Simulation_State "wikilink") for saving the current simulation state.

<!-- -->

-   Tools
    -   [tls_csv2SUMO.py](/Tools/tls#tls_csv2SUMO.py "wikilink") now handles controlled edges within a joined traffic light definition automatically.
    -   Added option to [netcheck.py](/Tools/Net#netcheck.py "wikilink"). This can be used to compute all components in the node graph without considering lane-to-lane connections.
    -   Added option to [generateBidiDistricts.py](/Tools/District#generateBidiDistricts.py "wikilink") (previously undocumented tool). This can improve opposite-finding in conjunction with option .
    -   Added option to [route2poly.py](/Tools/Routes#route2poly.py "wikilink"). This can be used to visualize routes from one network within another network.

### Other

-   Miscellaneous
    -   Visual Studio project files have been updated MSVC12. While it is still possible to build SUMO with MSVC10, this support may be dropped in the future in favor of C++11.

<!-- -->

-   Simulation
    -   When [saving simulation state](/Simulation/SaveAndLoad "wikilink") as *XML*, lane elements now contain their id for easier inspection.
    -   The [departPos](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#departPos "wikilink") values , and were removed since they never worked as intended.
    -   Option is now deprecated.

<!-- -->

-   SUMO-GUI
    -   Vehicle type parameters were moved to a separate dialog box (*Show Type Parameter*).

<!-- -->

-   TraCI
    -   TraCI version is now 11.

<!-- -->

-   Documentation
    -   Added page on [saving and loading simulation state](/Simulation/SaveAndLoad "wikilink")
    -   [Arrival parameters are now documented](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#A_Vehicle.27s_depart_and_arrival_parameter "wikilink")
    -   Extended [NETEDIT](/NETEDIT "wikilink") documentation.
    -   Described [netdiff.py](/Tools/Net#netdiff.py "wikilink"), a tool for comparing networks which was undocumented for a long time.
    -   Added page on [modelling networks for motorway simulation. In particular on-off-ramps](/Simulation/Motorways#Building_a_network_for_motorway_simulation "wikilink")
    -   Added new [overview page for usage of elevation data](/Networks/Elevation "wikilink")
    -   Added documentation [on influencing the simulation via SUMO-GUI](/SUMO-GUI#Influencing_the_simulation "wikilink")
    -   Added detailed [License](/License "wikilink") information.
    -   All applications report some build configuration when called without options.
