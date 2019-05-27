---
title: Z Changes from Version 0.29.0 to Version 0.30.0
permalink: /Z/Changes_from_Version_0.29.0_to_Version_0.30.0/
---

Version 0.30.0 (02.05.2017)
---------------------------

### Bugfixes

-   Simulation
    -   Random pedestrian decelerations (configured via option ) are now working.
    -   Loading state-files with vehicles that stop at a is now working.
    -   Fixed collisions when using the sublane model. ,, ,
    -   Various fixes to lateral distance keeping in the sublane model.
    -   Vehicles now longer drive beyond the road borders when using the sublane model.
    -   Fixed crash when loading saved stated with an arriving vehicle.
    -   Option now properly applies to vehicles departing in the future that are part of the loaded state (i.e. due to having been loaded from an additional file before saving). This was a regression in version 0.29.0.
    -   Simulation behaviour is no longer affected by randomly equipping vehicles with devices that only generate outputs.
    -   vType-attribute is no longer ignored (was silently replaced with “default”, since version 0.28.0)
    -   Fixed deadlock when setting vehicle attributes *arrivalSpeed* and *arrivalPos* both to 0.
    -   Fixed issue where a lane-change was blocked for invalid reasons causing deadlock.
    -   When using , the look-ahead distance is now limited to 3000m for determining suitable insertion lanes.
    -   loading state now writes tls states correctly

<!-- -->

-   NETCONVERT
    -   Various fixes to junction-shape computation. , ,
    -   Ramp-guessing (option ) no longer identifies sharply turning roads as motorway ramps.
    -   Fixed invalid right-of-way rules at junctions with type *traffic_light_right_on_red* when importing a *net.xml* file or editing with [NETEDIT](/NETEDIT "wikilink").
    -   Networks built with option now retain their shape when imported again.
    -   Networks [imported from VISUM](/Networks/Import/VISUM "wikilink") no longer round node positions to meters.
    -   Loading *.tll* files from a network that includes node types or is now working.
    -   Fixed crash when applying a to an edge within a roundabout.
    -   Fixed infinite loop when importing some OpenDRIVE networks.

<!-- -->

-   NETEDIT
    -   [vClass-specific speed limits](/Networks/Building_Networks_from_own_XML-descriptions#vehicle-class_specific_speed_limits "wikilink") are no longer lost when saving a network.
    -   The lane shapes induced by option are no longer lost when editing a network
    -   Deleting whole edges is working again (regression in 0.29.0).
    -   Deleting edges and afterwards adding edges no longer creates node type “unregulated” (without right-of-way rules).
    -   Fixed visual glitches when opening left-hand networks.
    -   Fixed various crashes. , , ,
    -   Fixed coloring of green-verge lanes.

<!-- -->

-   TraCI
    -   Fixed mapping failures when calling *moveToXY*.
    -   Vehicles that are moving outside the road network due to *moveToXY* calls now return the correct position and angle.
    -   Function *vehicle.getSpeedWithoutTraCI* now correctly returns the current speed if the vehicle is not being influenced.
    -   Fixed crash when adding and erasing persons in the same step.

<!-- -->

-   Tools
    -   Restored Python3.0 compatibility for sumolib and traci (regression in 0.29.0)
    -   carFollowing child-elements of vType element are now included in route2trips.py output.
    -   Fixed OSM Web Wizard problems with spaces in SUMO_HOME path.
    -   [cutRoutes.py](/Tools/Routes#cutRoutes.py "wikilink") now writes two independent routes instead of one containing edges not contained in the reduced network.

### Enhancements

-   Simulation
    -   [vClass-specific speed limits](/Networks/Building_Networks_from_own_XML-descriptions#vehicle-class_specific_speed_limits "wikilink") can now be loaded from an .
    -   Refactored implementation of [E2 detectors](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink"). These may now be defined to span over a sequence of lanes, XML-attribute is deprecated. , , ,
    -   Added [traffic light type “delay_based”](/Simulation/Traffic_Lights#Based_on_Time_Loss "wikilink") which implements an alternative algorithm to type “actuated”.
    -   Added option which defines the waiting time until driver impatience grows from 0 to 1. Formerly this was tied to the value of .
    -   [lanechange-output](/Simulation/Output/Lanechange "wikilink") now includes the lateral gap to the closest neighbor.
    -   [attribute ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Speed_Distributions "wikilink") can use normal distributions with optional cutoff to define the distribution of vehicle speeds
    -   [Traffic light related outputs](/Simulation/Output/Traffic_Lights "wikilink") have now consistent camelCase XML tags.
    -   Added option which lets vehicles stop for a time after experiencing a collision before the action set via takes place.
    -   [Electric vehicles](/Models/Electric "wikilink") are now initialized with a maximum capacity of 35kWh and and a half full battery by default (before, the default was 0 which always made it necessary to define this).
    -   now includes additional vehicle attributes such as *departLane* and *departSpeed* to facilitate scenario replaying.

    -   Increased maximum possible insertion flow when using *departLane* values *free,allowed* or *best* on multi-lane edges.
    -   Improvements to lateral-gap keeping when using the [sublane model](/Simulation/SublaneModel "wikilink"):
        -   Vehicles now attempt to equalize left and right gaps if there is insuffient lateral space
        -   The semantics of attribute where changed to define the desired gap at 50km/h and do not grow beyond that speed (before that threshold was at 100km/h)
        -   Vehicles now ignore follower vehicles behind the midpoint of their own length in regard to lateral gap keeping.
    -   Added option which can abort the simulation after a number of teleports is exceeded.
    -   Added option which generates output for [chargingStations](/Models/Electric#Charging_Station_output "wikilink").

<!-- -->

-   SUMO-GUI
    -   Added parameters *minGapLat,maxSpeedLat,latAlignment,boardingDuration,loadingDuration,car follow model* to the vType-parameter window.
    -   Added parameter *acceleration* to the vehicle-parameter window.
    -   Added option *Show type parameter dialog* to the person context menu.
    -   When running the simulation with option , the average travel speed of completed trips is shown in the network parameter dialog.
    -   For long-running simulations the time displays can now show elapsed days.

<!-- -->

-   NETCONVERT
    -   Networks imported from [DlrNavteq](/Networks/Import/DlrNavteq "wikilink")-format now process *prohibited_manoeuvres* and *connected_lanes* input files.
    -   Edge types are now imported from a *.net.xml* file.
    -   Added option for setting the level of detail when importing road geometries from parmeterized curves.
    -   Node shape computation (especially stop line position) can now be influenced by setting edge geometries that do not extend to the node position.
        -   To deal with ambiguous stop line information in OpenDrive networks, the new option may now now be used to affect the heuristic that computes stop line positioning based on the border between roads and connecting roads.
    -   Bus stops can now be imported from OpenStreetMap using the new option .
    -   Lanes within a network that have no incoming connection and edges that have no outgong connections are now reported.
    -   Specific lanes can now be deleted [via loaded *.edg.xml* files](/Networks/Building_Networks_from_own_XML-descriptions#Deleting_edges_or_lanes "wikilink") (to ensure that connections are kept as intended).

<!-- -->

-   NETEDIT
    -   The junction visualization options *show link junction index* and *show link tls index* are now working
    -   When creating or moving edge and junction geometry, positions can now be [restricted to a regular grid](/NETEDIT#Background_Grid "wikilink") (i.e. multiples of 100).
    -   [Custom edge geometry endpoints](/NETEDIT#Specifying_the_complete_geometry_of_an_edge_including_endpoints "wikilink") values can now be entered in inspect mode.

<!-- -->

-   TraCI
    -   It is now possible to reload the simulation with new options by sending the [load command](/TraCI/Control-related_commands#Command_0x01:_Load "wikilink").
    -   Added *vehicle.setMaxSpeed* and *vehicle.getMaxSpeed* to the C++ client. Thanks to Raphael Riebl for the patch.
    -   Added *vehicle.changeTarget* to the C++ client.
    -   To allow vehicles to run a red light, speedmode *7* can now be used instead of *14*. This is much safer as it avoids rear-end collisions.
    -   Vehicles can now stop at a named ParkingArea or ChargingStation. The methods *traci.vehicle.setParkingAreaStop, traci.vehicle.setChargingStationStop* were added to the python client to simplify this.
    -   vehicle function *moveToXY* now supports the special angle value *traci.constants.INVALID_DOUBLE_VALUE*. If this is set, the angle will not be factored into the scoring of candidate lanes and the vehicle will assume the angle of the best found lane. For vehicles outside the road network, the angle will be computed from the old and new position.
    -   Vehicles now support [retrieval of battery device parameters and retrieval of riding persons and containers as well as retrieval of laneChangeModel parameters](/TraCI/Vehicle_Value_Retrieval#Device_and_LaneChangeModel_Parameter_Retrieval_0x7e "wikilink") using the *vehicle.getParameter* function.
    -   Vehicles now support [setting of battery device parameters and laneChangeModel parameters](/TraCI/Change_Vehicle_State#Setting_Device_and_LaneChangeModel_Parameters_.280x7e.29 "wikilink") using the *vehicle.setParameter* function.
    -   Added [sublane-model related](/Simulation/SublaneModel "wikilink") vehicle functions *getLateralLanePosition, getMaxSpeedLat, getMinGapLat, getLateralAlignment, setMaxSpeedLat, setMinGapLat, setLateralAlignment, changeSublane*. ,
    -   Added [sublane-model related](/Simulation/SublaneModel "wikilink") vehicletype functions *getMaxSpeedLat, getMinGapLat, getLateralAlignment, setMaxSpeedLat, setMinGapLat, setLateralAlignment*.
    -   Function *edge.getLastStepPersonIDs* now includes persons riding in a vehicle which are on that edge.
    -   The TraCI python client now supports [StepListeners](/TraCI/Interfacing_TraCI_from_Python#Adding_a_StepListener "wikilink").
    -   The lane-changing choices of the laneChange model can now be retrieved (with and without TraCI influence) using [command *change lane information 0x13*](/TraCI/Vehicle_Value_Retrieval "wikilink").

<!-- -->

-   Miscellaneous
    -   Improved routing efficiency of [SUMO](/SUMO "wikilink"),[DUAROUTER](/DUAROUTER "wikilink") and [MAROUTER](/MAROUTER "wikilink") when using option .

<!-- -->

-   Tools
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") now supports the option to generate a number of random flows instead of individual vehicles.
    -   [routeStats.py](/Tools/Routes#routeStats.py "wikilink") now supports generating statistics on departure time by setting the option .
    -   [tls_csv2SUMO.py](/Tools/tls#tls_csv2SUMO.py "wikilink") can now take arbitrary strings as index and has improved signal group handling, thanks to Harald Schaefer
    -   more tools (including osmWebWizard) are python3 compatible

### Other

-   Documentation
    -   The [TraCI command documentation](/TraCI#TraCI_Commands "wikilink") now includes links to the corresponding python functions for each command.
    -   New [overview page on safety-related behavior](/Simulation/Safety "wikilink")
    -   The [Quick Start tutorial](/Tutorials/quick_start "wikilink") now describes how to create an network with [NETEDIT](/NETEDIT "wikilink")

<!-- -->

-   TraCI
    -   TraCI version is now 15
    -   some TraCI constants have been renamed
        -   CMD_SIMSTEP2 to CMD_SIMSTEP
        -   -   AREAL_DETECTOR\* to \*LANEAREA\*

        -   -   MULTI_ENTRY_EXIT_DETECTOR\* TO \*MULTIENTRYEXIT\*

<!-- -->

-   Miscellaneous
    -   The compile-option was removed. Simulation without internal lanes is still possible using either the netconvert option or the simulation option
    -   The compile-option and the corresponding nvwa package were removed. Checking for memory leaks should be done using the clang build or valgrind.
