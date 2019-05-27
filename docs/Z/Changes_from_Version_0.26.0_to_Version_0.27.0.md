---
title: Z Changes from Version 0.26.0 to Version 0.27.0
permalink: /Z/Changes_from_Version_0.26.0_to_Version_0.27.0/
---

Version 0.27.0 (12.07.2016)
---------------------------

### Bugfixes

-   Simulation
    -   Attribute is now used when routing trips and flows within the simulation.
    -   Vehicles stopping at a now reach the exact location when using sub-second step-lengths.
    -   Vehicles are no longer considered stopped at a while still driving with high speed.
    -   Scheduled [stops](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink") no longer count towards *waitSteps* and *timeLoss* in [tripinfo-output](/Simulation/Output/TripInfo#Generated_Output "wikilink").
    -   Fixed bug where vehicles would not depart from a triggered stop
    -   Fixed deadlock when vehicles with triggered stops could not load passengers or containers due to capacity constraints.
    -   Fixed invalid edge travel times used for dynamic routing in case flow differs among the lanes.
    -   Fixed invalid edge travel times used for dynamic routing due to invalid averaging
    -   Fixed invalid time stamps for leave times and an off by one for instant induction loops

<!-- -->

-   MESO
    -   The jam-front back-propagation speed now reaches realistic values (it was illogically low before). Note that default value of option changes as well as it's semantics.
    -   Fixed bug where the simulation would not terminate when using calibrators.
    -   The options and now define net time gaps (default values were changed accordingly). The gross time gaps are computed based on vehicle lengths and edge speed to allow for more realistic flow in networks with widely varying speed limits. This also affects the threshold that defines jamming when using default options (thresholds based on allowed speeds).

<!-- -->

-   NETCONVERT
    -   Fixed connection-guessing heuristic. , , ,
    -   Option is now working when loading a *.net.xml* file.
    -   Fixed bugs when importing cycleways from OSM.
    -   Option now records original edge ids even if input edges were joined.
    -   Fixed invalid road types when exporting OpenDRIVE networks.
    -   Fixed invalid lane permissions due to invalid removal of geometry-like nodes.

<!-- -->

-   SUMO-GUI
    -   Fixed crash when loading a large number of background images.
    -   Fixed persons showing up too early in the locator.

<!-- -->

-   NETEDIT
    -   Fixed crash when trying to set an empty string as edge length or edge width.
    -   Fixed crash when deleting the last lane of an edge.

<!-- -->

-   DUAROUTER
    -   Trips and flows that use attribute to loop over the destination edge more than once are now working.

<!-- -->

-   MAROUTER
    -   The output is now correctly sorted when using trips as input.

<!-- -->

-   POLYCONVERT
    -   Polyconvert output files can now be imported again by Polyconvert (i.e. for further transformations).

<!-- -->

-   TraCI
    -   Fixed *route.add*, *gui.screenshot* and *gui.trackVehicle* and various *lane* commands for the [C++ TraCI API client](/TraCI/C%2B%2BTraCIAPI "wikilink")
    -   Fixed crash when trying to set invalid routes.
    -   Fixed invalid values when retrieving edge mean speed and edge travel time in case flow differs among the lanes.
    -   Fixed retrieval of exit times for vehicles that spend multiple steps on an inductionloop when retrieving *last step vehicle data (0x17)*.

### Enhancements

-   Simulation
    -   Added [model for sublane-simulation](/Simulation/SublaneModel "wikilink"). This is activated by setting the option . When using this option, vehicles may move laterally within their lanes. This is influenced by the new [vType-attributes *latAlignment*, *maxSpeedLat*, *minGapLat*](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink"). Lane changing is performed according to the new lane changing model [SL2005](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink").
    -   Lane-changing models can now be configured with additional parameters. There exists [one parameter for each of the lane-changing motivations](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink") *strategic,cooperative,speedGain* and *keepRight* which can be used to increase or reduce that type of lane changing.
    -   Added capabilities for [overtaking through the opposite-direction lane](/Simulation/OppositeDirectionDriving "wikilink").
    -   Added new option for configuring the action to take on vehicle collision. Allowed actions are *none,warn,teleport* and *remove*. The default is *teleport* which moves the rear vehicle involved in a collision onto a subsequent lane (as before).
    -   Added new option to enable geometrical collision checking on junctions. By default this option is set to *false* and collisions between non-consecutive lanes are ignored as before. This option may slow down the simulation.
    -   ChargingStations [can now be used to declare vehicle stops](/Models/Electric#Stopping_at_a_Charging_Station "wikilink").
    -   the [vehicle route output](/Simulation/Output/VehRoutes "wikilink") now includes optional vehicle parameters as entries
    -   Added new option to switch the default algorithm for averaging edge travel times from exponential averaging to a moving average over the given number of steps.
    -   Added new option for switching off all traffic lights (the traffic lights can still be switched on via GUI or TraCI).
    -   Added new [output for tracking lane change events](/Simulation/Output/Lanechange "wikilink"). This is enabled using the new option .

<!-- -->

-   MESO
    -   The option now gives additional freedom when configuring a speed dependent jam-threshold. When an value below 0 is given the absolute value is taking as a factor for the minimum unjammed speed. Thus, negative values closer to 0 result in less jamming. The default value remains at *-1* and results in the original behaviour (values above 0 set the occupancy fraction threshold independent of edge speed as before).

<!-- -->

-   SUMO-GUI
    -   The number of running vehicles and persons is now shown in the status bar. This display also acts as a button for opening the network parameter dialog.
    -   [Charging stations](/Models/Electric#Charging_Stations "wikilink") are now shown in a different color when active.
    -   Persons are now more visible when selecting *Draw with constant size when zoomed out*.
    -   Added the averaged speeds that are used for [simulation routing](/Demand/Automatic_Routing "wikilink") to the lane parameter dialog.
    -   Added new option which automatically reloads and starts the simulation every time it ends.

<!-- -->

-   MESO-GUI
    -   Can now color edges by the averaged speeds that are used for [simulation routing](/Demand/Automatic_Routing "wikilink").
    -   Can now color edge segments (mesoscopic vehicle queues) individually by various traffic measures.

<!-- -->

-   NETCONVERT
    -   Added option for setting the default width of lanes (also applies to [NETGENERATE](/NETGENERATE "wikilink")).
    -   Added option for forcing all node and edge IDs to be integers (also applies to [NETGENERATE](/NETGENERATE "wikilink")).
    -   Added Option to avoid negative speeds when using Option .

<!-- -->

-   NETEDIT
    -   Many additional network structures such as busStops, detectors and variable speed signs can now be defined and manipulated.

<!-- -->

-   NETGENERATE
    -   Added option for using a chess-like intersection naming scheme (A1, B3, etc).

<!-- -->

-   TraCI
    -   Added [vehicle command](/TraCI/Vehicle_Value_Retrieval "wikilink") *next TLS* to retrieve upcoming traffic lights along a vehicles route.
    -   The [vehicle command](/TraCI/Change_Vehicle_State#move_to_XY_.280xb4.29 "wikilink") *move to XY* (formerly *move to VTD*) now supports an additional flag which selects whether the original route shall be kept or the route may change and whether the vehicle may leave the road network. ,
    -   The [vehicle command](/TraCI/Change_Vehicle_State#move_to_XY_.280xb4.29 "wikilink") *move to XY* now allows moving vehicles that are still in the insertion buffer.
    -   Added functions *vehicle.add, vehicle.remove* and *vehicle.moveToXY* to the [C++ TraCI API client](/TraCI/C%2B%2BTraCIAPI "wikilink")
    -   Added object variable subscriptions and context subscriptions to the C++ TraCI-library (*subscribe, getSubscriptionResults, subscribeContext, getContextSubscriptionResults*). Thanks to Erik Newton for the patch.
    -   Added person value retrieval functions to the [C++ TraCI API client](/TraCI/C%2B%2BTraCIAPI "wikilink"). Thanks to Caner Ipek for the patch.
    -   Added [vehicle command](/TraCI/Vehicle_Value_Retrieval "wikilink") *get speedmode 0xb3* to retrieve the [speed mode](/TraCI/Change_Vehicle_State#speed_mode_.280xb3.29 "wikilink") of vehicles.
    -   Added [vehicle command](/TraCI/Vehicle_Value_Retrieval "wikilink") *get slope 0x36* to retrieve the slope at its current position
    -   Added [vehicle](/TraCI/Vehicle_Value_Retrieval "wikilink"), [lane](/TraCI/Lane_Value_Retrieval "wikilink") and [edge](/TraCI/Edge_Value_Retrieval "wikilink") command *get electricity consumption 0x71* to retrieve the electricity consumption if the emission model supports it.
    -   Multiple subscriptions for the same object are now merged.

<!-- -->

-   Tools
    -   Added new tool [createVehTypeDistributions.py](/Tools/Misc#createVehTypeDistributions.py "wikilink") to simplify definition of heterogeneous vehicle fleets by sampling numerical attributes from configurable distributions. Thanks to Mirko Barthauer for the contribution.
    -   parsing xml files with [sumolib.output.parse()](/Tools/Sumolib "wikilink") is now much faster.

### Other

-   Documentation
    -   Test coverage analysis can now be found at [1](http://sumo.dlr.de/daily/lcov/html/).
    -   Documented [Wireless device detection model](/Simulation/Bluetooth "wikilink") which has been available since version 0.18.0

<!-- -->

-   NETCONVERT
    -   Network version is now 0.27.0

<!-- -->

-   TraCI
    -   TraCI version is now 12.
    -   The [vehicle command](/TraCI/Change_Vehicle_State "wikilink") *move to VTD* is now referred to as *move to XY* in client code.
