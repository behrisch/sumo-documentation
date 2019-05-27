---
layout: post
title: ChangeLog
permalink: /ChangeLog/
---

Git master
----------

### Bugfixes

-   Simulation
    -   All car-following models now respect the vType-attribute *emergencyDecel* as an absolute bound on deceleration.
    -   Fixed collisions when using [continous lane change](/Simulation/SublaneModel#Simple_Continous_lane-change_model "wikilink").
    -   Fixed back-and-forth changing when using [continous lane change](/Simulation/SublaneModel#Simple_Continous_lane-change_model "wikilink").
    -   Fixed loading of teleporting vehicles from simulation state in *.sbx* format.
    -   Fixed invalid vehicle counts by E2-detector related to lane-changing.
    -   Fixed invalid vehicle counts by E3-detector related to re-using vehicle pointers ,
    -   Fixed bug that was causing invalid slowdown while passing an intersection.
    -   Fixed bug that was causing pedestrians on looped routes to block themselves.
    -   Vehicle speedFactor is now included in saved state.
    -   Fixed invalid collision events when lanes are to narrow for the vehicles.
    -   Fixed collision between pedestrians and vehicles.
    -   Fixed bug where option would trigger invalid warnings regarding unsorted route file.
    -   Fixed invalid stopping position after collision when using option
    -   Fixed right-of-way rules for vehicles standing next to each other on the same lane and driving towards different edges.
    -   Fixed crash within intersection between vehicles coming from the same lane.
    -   Fixed invalid *departDelay* for triggered vehicles.

<!-- -->

-   SUMO-GUI
    -   width of railway edges is now taken into account when drawing (interpreted as gauge).
    -   window-size and position now remain unchanged when reloading the simulation.
    -   Random vehicle and person coloring is now more random on windows.
    -   Vehicles that were not inserted (i.e. due to option or ) no longer count as *arrived* in the simulation parameter dialog. Instead the are counted under the new item *discarded vehicles*.
    -   Fixed issues related to drawing smooth corners at curving roads.
    -   Fixed vehicle positions when using the sublane model in lefthand networks.
    -   Fixed crashing and visualization problems when using the 3D-view. ,
    -   Fixed glitch where persons would appear to jump around while riding in a vehicle across an intersection.
    -   Tracking of riding persons now centers on the person rather than the front its vehicle.
    -   ChargingStation are visible again (regression in 0.32.0)

<!-- -->

-   MESO
    -   Fixed deadlock at roundabouts when running with option or .

<!-- -->

-   NETEDIT
    -   Splitting edges, deleting individual edges and lanes or adding lanes via the *duplicate* menu option no longer resets connections and traffic light plans.
    -   The viewing area and zoom loaded via option is no longer ignored
    -   Fixed bug where connections on large junctions did not register clicks or were not drawn.
    -   Fixed crash when removing inspected object via *undo*.
    -   Fixed various bugs that led to re-computation of signal plans when modifying connections or tls indices. ,
    -   Fixed bug that could lead to the creation of invalid networks when adding and removing connections. ,
    -   Custom connection shape is now longer lost after *delete*+*undo*.
    -   Splitting edges no longer introduces unnecessary custom endpoints.
    -   Fixed inverted interpretation of *lanePosLat* for POIs compared to SUMO-GUI.
    -   Fixed crash when deleting one of multiple signal programs for the same junction.

<!-- -->

-   NETCONVERT
    -   Option no longer builds ramps at traffic light controlled nodes.
    -   Fixed bug that was causing invalid link states at intermodal junctions.
    -   Fixed bugs that were causing invalid link directions.
    -   Fixed invalid junction logic in lefthand networks.
    -   Generated signal plans will no longer have a protected left-turn phase if there is no dedicated left-turn lane.
    -   Various fixes in regard to classifying nodes as type *rail_crossing* and joining clusters of rail crossing nodes.
    -   Option is now working when loading a *.net.xml* file.

<!-- -->

-   DUAROUTER
    -   Fixed crash on intermodal routing.

<!-- -->

-   POLYCONVERT
    -   Fixed bug when importing OSM data with objects that are marked as *deleted*.

<!-- -->

-   TraCI
    -   Fixed bug where persons would “jump” when replacing the current walking stage with a new one.
    -   Fixed crash when trying to access empty subscription result list using the C++ client.
    -   Vehicle *emergencyDecel* is now at least as high as *decel* after calling *traci.vehicle.setDecel*.
    -   Fixed python client bug in *traci.polygon.setShape*.
    -   Adding a route with an empty list of edges now results in an error.
    -   Vehicles that drive outside the road network under the control of *moveToXY* now properly updated their speed and brake lights.
    -   Function *vehicle.getLaneChangeMode* now returns correct values for the original lane change state when the state is affected by *vehicle.setLaneChangeMode*.
    -   Car-following related vehicle type parameters (e.g. *accel*) that are changed via traci are now correctly saved when saving simulation state.
    -   When using context subscriptions around an object, that object itself is no longer included in the result.
    -   Functions *simulation.findRoute* and *simulation.findIntermodalRoute* no longer crash sumo when trying to route from a forbidden edge.
    -   Fixed invalid results when calling *simulation.findIntermodalRoute* ,,

<!-- -->

-   Tools
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") now uses vType attributes from option when generating persons.

### Enhancements

-   All applications
    -   All time values in options and xml inputs can now be specified in the format *h:m:s* and *d:h:m:s* (where the values for days, hours and minutes are all positive integers and seconds may also be a positive floating point number).
    -   Added option (short ) that causes all time values to be written in h:m:s (or d:h:m:s) format.

<!-- -->

-   Simulation
    -   Tripinfo-output now includes the attribute *stopTime* which records the time spent with intentional stopping.
    -   A pedestrian crossings can now have different signal states for both directions.
    -   FCD-output can now be switched on selectively for a subset of vehicles and the reporting period can be configured.
    -   Intended departure times (attribute *depart*) and intended vehicle id (attribute *intended*) are now added to vehroute-output of public transport rides.
    -   Stopping place names are now added as XML-comments in vehroute-output of public transport rides.
    -   Lane-Change-Model parameter *lcTurnAlignmentDistance* added for the control of dynamic alignment in simulations using the sublane model, see [Lane-Changing Models](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink"), .
    -   Implemented [SSM Device](/Simulation/Output/SSM_Device "wikilink"), which allows output of saftey related quantities.
    -   [Statistic output](/Simulation/Output#Aggregated_Traffic_Measures "wikilink") now also includes total delay by vehicles which could not be inserted by the end of the simulation if options and are set.
    -   The default lane-changing model *LC2013* now supports [parameter *lcAssertive*](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink").

<!-- -->

-   SUMO-GUI
    -   Added control for scaling traffic demand dynamically.
    -   Added option to disable drawing of bicycle lane markings on intersections.
    -   All laneChangeModel-related vType-parameters and all junction-model related vType-parameters are now shown in the vType-Parameter dialog.
    -   The simulation view can now be rotated via the new gui-settings attribute *angle* in the or via the viewport dialog.
    -   When drawing junction shapes with exaggerated size and setting option *show lane-to-lane connections*, the connecting lines are now scaled up at traffic light junctions.
    -   The simulation state can now be saved via the *Simulation* Menu.
    -   Object tracking can now be aborted via double-click.
    -   Person plans can now be inspected via the right-click menu.
    -   Object name rendering size can now be toggled between constant pixel size (all visible when zoomed out) and constant network size (invisible when zoomed out).
    -   The *Delay* value is now invariant with regard to the simulation step length and always denotes delay per simulated second.

<!-- -->

-   MESO
    -   Simulation of persons and public transport is now supported.

<!-- -->

-   NETEDIT
    -   Added virtual attribute to identify [bidirectional rail edge pairs](/Simulation/Railways#Bidirectional_track_usage "wikilink").
    -   Added option to modify the visualisation of [bidirectional rail edge pairs](/Simulation/Railways#Bidirectional_track_usage "wikilink") (*spread superposed*)
    -   Added button *add states* to *traffic light*-mode to complement the functionality of *cleanup states*.
    -   Netedit now flags connection targets with incompatible permissions as *conflict* and only creates them with *<ctrl>+<click>*.
    -   Traffic light indices are now drawn for pedestrian crossings when enabled via gui settings.
    -   Now ParkingAreas and ParkingSpaces can be created in netedit.
    -   When adding a new phase to a traffic light, the new phase will now have a plausible successor state depending on the selected previous phase (rather the being a copy).
    -   Added function 'split' to junction context menu. This can be used to disaggregated joined junctions.
    -   When joining traffic lights (by editing junction attribute 'tl'), link indices of the target traffic light are now preserved if signal groups are used (multiple connections with the same *linkIndex* value). .

<!-- -->

-   NETCONVERT
    -   Geo-referenced networks (i.e. from OSM) can now be merged by loading them together ().
    -   Element now supports attribute *linkIndex2* to specify a custom signal index for the reverse direction.
    -   When defining [double connections](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink"), the right-of-way rules now take the road topology into account to differentiate between on-ramp and off-ramp situations.
    -   Importing VISUM networks up to format version 10 is now support.
    -   Improved heuristics for options .
    -   Improved computation of intermodal junctions imported from OSM.
    -   Improved computation of junction shapes.
    -   Added option for rotating the network.
    -   Added option which can be used to add a prefix to the written junction and edge IDs.
    -   Added options to control the timing of pedestrian crossing phases.
    -   Added option to ensure that left turns through oncoming traffic are not build for high-speed roads.
    -   Sidewalk information is now imported from OSM for road types that have a positive sidewalkWidth attribute (e.g. by using typemap [osmNetconvertPedestrians.typ.xml](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink")).
    -   Added option for increasing the length of stop access edges above the airline distance. .
    -   Added option which sets an upper bound on speed while passing an intersection based on the turning radius.

<!-- -->

-   NETGENERATE
    -   Simplified node and edge names
        -   The alphanumerical junction naming scheme now supports arbitrary grid sizes (using ids like *XY23*)
        -   The alphanumerical junction naming scheme also extends to spider networks
        -   The alphanumerical junction naming scheme is active by default (the option for enabling the old scheme was renamed from to ).
        -   When using alphanumerical junction ids, the intermediate string *to* is omitted from edge names because the edge ID already allows unambiguous determination of its junctions without it
    -   Added option to randomize lane numbers in random networks between 1 and *default.lanenumber*
    -   Added option to edge priorities in random networks between 1 and *default.priority*
    -   Added option to place generated junctions on a regular grid
    -   Added option which can be used to add a prefix to the generated junction and edge IDs.
    -   Corridor networks can now be generated by using options such as
    -   Added options and to add left-turn lanes to generated networks.

<!-- -->

-   DUAROUTER
    -   Intended departure times (attribute *depart*) and intended vehicle id (attribute *intended*) are now added to vehroute-output of public transport rides.
    -   Stopping place names are now added as XML-comments in route-output of public transport rides.

<!-- -->

-   TraCI
    -   function *vehicle.add* now supports using the empty string ("") as a route id to insert the vehicle on an arbitrary valid edge. This makes it easier to remote-control vehicles using moveToXY without defining an initial route.
    -   added functions *simulation.getCollidingVehiclesNumber* and *simulation.getCollidingVehiclesIDList* to track collisions.
    -   added function *edge.getLaneNumber* to retrieve the number of lanes of an edge.
    -   added function *vehicle.getAcceleration* to retrieve the acceleration in the previous step.
    -   added function *gui.hasView* to determine whether graphical capabilities exist.
    -   function *simulation.getMinExpectedNumber()* now includes persons that are still active in the simulation.
    -   added function *traci.getLabel* to the python client to help working with multiple connections.

<!-- -->

-   Tools
    -   sumolib now supports lane.getWidth().
    -   webWizard now correctly builds regions with left-hand traffic
    -   Additional options for [generateTLSE3Detectors.py](/Tools/Output#generateTLSE3Detectors.py "wikilink") that make it suitable for generating various kind of junction related output.

### Other

-   Documentation
    -   Added [documentation on joined traffic lights and defining signal groups](/Simulation/Traffic_Lights "wikilink").
    -   Added [documentation on the simple continous lane-change model](/Simulation/SublaneModel#Simple_Continous_lane-change_model "wikilink").
    -   Documented all supported [routing algorithms](/Simulation/Routing#Routing_Algorithms "wikilink").

<!-- -->

-   Simulation
    -   tripinfo-output attribute *waitSteps* which counts the number of simulation steps in which the vehicle was below a threshold speed of 0.1m/s was replaced by attribute *waitingTime* which measures the same time in seconds. This gives results which are independent of the simulation parameter.
    -   The default value for option was changed from *1* to *60* to speed up simulation.

<!-- -->

-   Miscellaneous
    -   The space character ' ' is no longer allowed in xml option values when separating file names. Instead the comma ',' must be used. Files with space in their path are now supported.
    -   NETCONVERT no longer creates an offset of 0.1m between lanes. This means the total visual width of an edge is now the sum of all lane widths. This also fixes an inconsistency between visualization and simulation as the vehicles always ignored this offset anyway. Road markings are now drawn on top of the lanes rather than between them. This causes small visual gaps in old networks (fixable by calling *netconvert -s old.net.xml -o new.net.xml*).

<!-- -->

-   TraCI
    -   TraCI Version is now 18

Version 0.32.0 (19.12.2017)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed collisions in the sublane model , ,
    -   Fixed bug that was causing invalid behavior in the sublane model when used with option .
    -   Fixed bug that was causing deadlocks after undercutting minimum gap.
    -   Fixed bug that was causing deadlocks at intersections.
    -   Option now also applies to invalid (i.e. misordered) stop definitions.
    -   PHEMlight handles large acceleration values better and has updated emission values for new Diesel cars
    -   definitions using attribute *until* that are used within a now shift the *until* times according to the offset between departure and flow *begin*.

    -   attribute *chargeDelay* now accepts floating point values.

    -   attribute *chargeDelay* now works with subsecond simulation.

    -   Vehicles passing a minor link with impatience 0 no longer force braking for prioritized vehicles.
    -   Fixed bug that was causing collisions between vehicles and pedestrians
    -   Fixed slow simulation when combining cars and ships in one simulation.
    -   Fixed collisions on junctions between vehicles coming from the same lane. ,
    -   Fixed failure to change lanes for speed gain in the sublane model.
    -   Fixed collision of a vehicle with itself.
    -   Several fixes in regard to intermodal routing. , , , ,

<!-- -->

-   SUMO-GUI
    -   Fixed crash when simulating pedestrians.
    -   Coloring *by selection* is now working for pedestrian crossings.
    -   Options and are now working when set in a configuration file.
    -   Vehicle blinkers that signal left or right turns now remain switched on while the vehicle is still on the intersection (requires networks to be rebuilt).
    -   Fixed invalid lane-change blinkers for near-zero lateral movements in the sublane model.
    -   Fixed invalid vehicle angle when using the sublane model.
    -   Networks created with simple projection can now be shown.
    -   Fixed invalid *duration factor* in network parameters for sub-second simulation.

<!-- -->

-   POLYCONVERT
    -   Fixed handling of XML special characters when exporting arbitrary text via option .

<!-- -->

-   NETCONVERT
    -   Fixed crash when importing Vissim networks.
    -   Fixed bug that was causing invalid signal plans when loading a .net.xml file and removing edges from an intersection with pedestrian crossings (the link indices for crossings were re-assigned but the signal plan was left unmodified creating a mismatch).
    -   No longer writing pedestrian crossings with length 0 (minimum length is 0.1m).
    -   Parameters (i.e. those for actuated traffic lights) are no longer lost when importing *.net.xml* files or *plain-xml* files.
    -   Fixed bug that was causing invalid networks to be generated when additional lanes were placed to the right of a sidewalk.
    -   Fixed bug that was causing invalid networks to be generated when nodes without connections were part of a joined traffic light
    -   Defining pedestrian crossings for [Pedestrian Scramble](https://en.wikipedia.org/wiki/Pedestrian_scramble) is now supported.
    -   Custom traffic light plans for pedestrian crossings are no longer modified.
    -   Fixed invalid traffic light plans at pedestrian crossings for node type *traffic_light_right_on_red*.
    -   Fixed invalid right of way rules at node type *traffic_light_right_on_red* that could cause deadlock.
    -   Networks with intersections that are very close to each other can now be re-imported.
    -   Edges that do not have connections are now correctly represented in plain-xml output.
    -   Fixed invalid geometry in opendrive-output for lefthand networks.
    -   Fixed invalid road markings in opendrive-output.

<!-- -->

-   NETEDIT
    -   Fixed bug that was causing pedestrian crossings to remain uncontrolled at traffic light controlled intersections.
    -   Options and are now working when set in a configuration file.
    -   Fixed crash when setting linkIndex.

<!-- -->

-   DUAROUTER
    -   Fixed invalid public transport routing if the last vehicle departs before the person enters the simulation.

<!-- -->

-   TraCI
    -   Fixed bug in *traci.trafficlights.setLinkState*.
    -   Fixed bug in *traci.vehicle.getDrivingDistance* related to internal edges.
    -   Fixed bug in *traci.vehicle.getDistance* related to looped routes.
    -   Fixed bug in *traci.simulation.getDistance2D* and *traci.simulation.getDistanceRoad* related to internal edges.
    -   Command *load* no longer fails when there are too many arguments or long file paths.
    -   Fixed bug in *traci.vehicle.changeLane* when using the sublane model.

<!-- -->

-   Tools
    -   Fixed bug that would trigger an infinite loop in [flowrouter.py](/Tools/Detector#flowrouter.py "wikilink").
    -   [ptlines2flows.py](/Tutorials/PT_from_OpenStreetMap "wikilink") fixes:
        -   missing stops no longer result in crashing
        -   fixed invalid *until* times when multiple lines use the same stop
    -   emissionsDrivingCycle now uses the slope values from the correct time step when forward calculation of acceleration is enabled
    -   [generateTurnDefs.py](/Tools/Misc#generateTurnDefs.py "wikilink") now writes interval information. Thanks to Srishti Dhamija for the patch.

### Enhancements

-   Simulation
    -   Added option to control whether collisions are registered when the vehicle *minGap* is violated. With the default value of 1.0 minGap must always be maintained. When setting this to 0 only *physical* collisions are registered.
    -   Added new [junction model parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Junction_Model_Parameters "wikilink") :
        -   *jmIgnoreFoeProb, jmIgnoreFoeSpeed* can be used to configure right-of-way violations.
        -   *jmSigmaMinor* allows configuring driving imperfection (dawdling) while passing a minor link.
        -   *jmTimegapMinor* configures the minimum time gap when passing a minor link ahead of a prioritized vehicle.
        -   *jmDriveAfterRedTime* and *jmDriveRedSpeed* allow configuring red-light violations depending on the duration of the red phase.
    -   Added new [laneChangeModel-attribute](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink") *lcLookaheadLeft* to configure the asymmetry between strategic lookahead when changing to the left or to the right.
    -   Added new [laneChangeModel-attribute](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink") *lcSpeedGainRight* to configure the asymmetry between thrhesholds when changing for speed gain to the left or to the right.
    -   [Electric vehicles](/Models/Electric "wikilink") can now be used for emission-model (electricity) output by setting
    -   Tripinfo-output for pedestrians now includes *routeLength, duration* and *timeLoss*.
    -   [duration-log.statistics](/Simulation/Output#Aggregated_Traffic_Measures "wikilink")-output now informs about person rides.
    -   Vehicles that end their route with a stop on a parkingArea (arrivalPos is within the parkingArea bounds) will be assigned a new destination after [rerouting to another parkingArea](/Simulation/Rerouter#Rerouting_to_an_alternative_Parking_Area "wikilink") (previously they would drive to the original parkingArea edge after finishing their stop).
    -   Rerouters now support the attribute which makes their activation dependent on on a minimum amount of accumulated waiting time.
    -   Simulation step length has been decoupled from the action step length, which is the vehicle's interval of taking decisions. This can be configured globally via the option '--default.action-step-length', or per vehicle via the parameter 'actionStepLength'.

<!-- -->

-   SUMO-GUI
    -   Transparency is now working for all objects.
    -   Junction parameters can now be inspected.
    -   Upcoming stops are now shown in the vehicle parameter window and also in the network when selecting *show current route*.

<!-- -->

-   NETCONVERT
    -   When using option together with option , the original IDs of all renamed nodes and edges are written to elements with key *origId*.
    -   connections now support the attribute *speed* to set a custom (maximum) speed on intersections.
    -   connections now support the attribute *shape* to set a custom shape.
    -   crossings now support the attribute *shape* to set a custom shape.
    -   The [new element ](/Networks/Building_Networks_from_own_XML-descriptions#Walking_Areas "wikilink") can now be used in *con.xml* files to define custom walking area shapes.
    -   Added options , , to set appropriate default stop lengths for different modes of traffic (in conjunction with option ).
    -   Added options which can be used to import additional edge parameters such as *bridge*, *tunnel* and *postcode*.
    -   Parallel lanes of connecting roads are now written as a single road in opendrive-output.

<!-- -->

-   NETEDIT
    -   Additional objects (i.e. detectors) as well as POIs and Polygons can now be located based on their ID.
    -   Connection and Crossing shapes can now be edited visually.
    -   Object types such as edges or polygons can now be locked against selection modification.
    -   The traffic light index of controlled connections can now be edited in *Inspect Mode*.
    -   Added button to traffic light mode for cleaning up unused states from a traffic light plan.

<!-- -->

-   DUAROUTER
    -   Vehicles and flows which are considered public transport (have the line attribute) are now only routed if an additional option is given.
    -   route alternative output (*.rou.alt.xml*) now contains costs for pedestrian stages.

<!-- -->

-   Tools
    -   [osmWebWizard.py](/Tools/Import/OSM#osmWebWizard.py "wikilink") can now import public transport (activated by a checkbox on the settings tab). If pedestrians are imported as well they may elect to use public transport to shorten their walks.
    -   added new tool [filterDistrics.py](/Tools/District#filterDistricts.py "wikilink") to generate district (TAZ) files that are valid for a given vehicle class
    -   [traceExporter.py](/Tools/TraceExporter "wikilink") can now built a direct socket connection to sumo and can filter fcd output for regions and times.
    -   [flowrouter.py](/Tools/Detector#flowrouter.py "wikilink") improvements:
        -   route and flow ids now include source and target edge ids for better readability.
        -   turn-around flow can now be limited using the new option
    -   Added [new tool **tls_csvSignalGroup.py** for importing traffic light definitions from csv input. The input format aims to be similar to the representation used by traffic engineers](/Tools/tls#tls_csvSignalGroup.py "wikilink"). Thanks to Mirko Barthauer for the contribution.

<!-- -->

-   TraCI
    -   return value of trafficlights.getControlledLinks is now a list of lists (of links) for the C++ client as well
    -   python client now supports the whole API for *vehicle.setAdaptedTraveltime* and *vehicle.setEffort* (resetting custom values or setting with default time range) by using default arguments.

### Other

-   The SUMO license changed to the [Eclipse Public License Version 2](https://eclipse.org/legal/epl-v20.html)
-   The SUMO build process now supports CMake. It is likely that version 0.32.0 will be the last one shipping Visual Studio solutions. Please have a look at [Installing/Windows_CMake](/Installing/Windows_CMake "wikilink") for information on how to build SUMO on Windows with CMake. There are also helper scripts in preparation at for instance .

<!-- -->

-   Simulation
    -   **chargingstations-output** now writes times as seconds rather than milliseconds.
    -   Default value of option changed to *0.64* (previously 0.65). This allows vehicles with default width to pass a pedestrian on a road with default width.
    -   preliminary version of [libsumo](/libsumo "wikilink") is available for experimental building of your own apps using SUMO as a “library” (calling its functions directly without TraCI)

<!-- -->

-   SUMO-GUI
    -   default font changed to [Roboto](https://fonts.google.com/specimen/Roboto)
    -   Removed OpenGL visualisation option *Antialias*
    -   E3-Entry and -Exit detectors are now drawn in darker color to better distinguish them from traffic lights.

<!-- -->

-   NETCONVERT
    -   The element is no longer supported. Instead and support the *shape* attribute. To set a custom shape for walkingAreas, the new element may be used.

<!-- -->

-   TraCI
    -   TraCI version is now 17

<!-- -->

-   Documentation
    -   Documented [simulation object right-click menus](/SUMO-GUI#Object_Properties_.2F_Right-Click-Functions "wikilink")
    -   Described [visualization of edgeData files](/SUMO-GUI#Visualizing_edge-related_data "wikilink")

Version 0.31.0 (14.09.2017)
---------------------------

### Bugfixes

-   Simulation
    -   [Sublane-model](/Simulation/SublaneModel "wikilink")
        -   Lane changing to clear the overtaking lane ([motivation *keepRight*](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink")) is now working properly.
        -   Fixed error that prevented violating right-of-way rules in the sublane-model.
        -   Fixed bug that was preventing speed adaptations for strategic changing.
        -   Fixed error that prevented changing for speed gain ,
        -   Insertion with is now working.
        -   Fixed bug that could cause deadlocks on an intersection
        -   Fixed collisions , , ,
        -   Fixed invalid angles when lane-changing at low speeds or low step-length.
        -   Fixed oscillation.
        -   Fixed too-late changing for speed gain when approaching a slow leader.
        -   Fixed bug that was causing sublane-changing despite speed loss.
    -   Lane-changing
        -   Fixed behavior problems in regard to the rule that prohibits overtaking on the right under some circumstances (by default this is prohibited in free-flowing motoroway traffic). Vehicles now avoid overtaking whenever braking is possible and they overtake on the left instead if there is a third lane. , , ,
        -   Fixed time loss due to late overtaking in some situations.
        -   Fixed invalid overtaking to the left. }
    -   Persons
        -   Attribute *arrivalPos* is no longer ignored for person elements.
        -   Fixed crash when pedestrian routes contain disallowed edges
        -   Fixed collision at prioritized crossings because pedestrians ignored some vehicles
    -   Calibrators now respect the option .
    -   no longer selects an invalid departLane on multimodal edge.

    -   Acquired waiting time of vehicles is now properly loaded from a simulation state.
    -   Fixed output of meso calibrator (regression in 0.30.0).
    -   Modified meanTimeLoss output of [lane area (e2) detector](/Simulation/Output/Lanearea_Detectors_(E2)#Generated_Output "wikilink"). Semantics is now average time loss \*per vehicle\*
    -   Fixed invalid stop state and invalid position of vehicles that cannot resume from parking due to blocking traffic.
    -   Fixed erroneous calculation of occupancy in meandata output for vehicles being only partially on the corresponding lane.
    -   Fixed collision detection of junctions (some collisions were not registered).
    -   Options is now working when collisions are detected on a junction (using Option ).
    -   FCD-output now contains z-data if the network includes elevation information.
    -   Fixed crash when loading invalid definition with element.
    -   Fixed invalid errors on loading stops on looped routes.
    -   Fixed crash on invalid definition.
    -   Fixed crash on saving and loading simulation state in conjunction with vehroute-output. ,
    -   Fixed too high density values in meandata output.
    -   Fixed invalid *routeLength* in tripinfo-output.

<!-- -->

-   SUMO-GUI
    -   Fixed visual glitch when drawing vehicles with multiple carriages as raster images.
    -   Fixed crash when reloading a simulation after editing the network.
    -   Fixed crash when using invalid routes in calibrator.
    -   The number of nodes listed in the network parameter dialog no longer includes internal nodes.
    -   Fixed crash when multiple vehicles start and end parking on the same edge
    -   All parking vehicles and empty parking spaces of a are now accessible via right-click.
    -   Fixed rendering position of on curved roads.
    -   Fixed drawing position of vehicles with lateral offset and of passengers if a vehicle is on a very short lane (also affects fcd-output).
    -   Corrected drawing of sublane borders in case the lane width is not a multiple of the lateral-resolution.
    -   Fixed wrong occupancy values in Parameter Window for short lanes.
    -   [Pre-configured screenshots](/SUMO-GUI#Screenshots "wikilink") are now taken at the correct time regardless of simulation speed.
    -   Fixed visual glitches when drawing waiting pedestrians, parking vehicles and parkingAreas in left-hand networks.
    -   The list of additional simulation objects no longer includes POIs and polygons (they have their own locator lists).

<!-- -->

-   Netconvert
    -   now exports stop lanes with the appropriate vClass.

    -   now exports stop lanes in the correct road direction ,

    -   Fixed invalid geo-reference when loading lefthand *.net.xml* files
    -   Fixed bug that was causing an error when patching a *.net.xml* file with a *.tll.xml* file along with other connection-affecting patches.
    -   Fixed insufficient precision of internal lane elevation in OpenDrive output.
    -   Fixed overly long yellow duration in generated tls plans.
    -   Fixed invalid lengths of internal turning lanes. As a side effect lane-changing is not possible any more while on these lanes. The old behavior can be enabled by setting option . .
    -   Variable phase durations are no longer lost when importing from *.net.xml* or *.tll.xml* files.
    -   Information about edges without connections is no longer lost when exporting with option .
    -   Fixed invalid edge shape after importing a *.net.xml* file with custom node shape.
    -   Fixes related to importing OpenDRIVE networks
        -   Fixed error when loading -data.
        -   Fixed crash when loading OpenDRIVE networks with attribute *pRange*.
        -   Fixed invalid traffic lights.
        -   Fixed invalid connections when importing OpenDRIVE networks
        -   Fixed invalid internal-lane speed when importing OpenDRIVE networks or setting lane-specific speeds.

<!-- -->

-   Netedit
    -   Fixed rendering slowdown (regression in 0.30.0)
    -   Fixed error when loading pois with attributes *lane* and *pos* (regression in 0.30.0)
    -   Fixed crash when trying to filter selection of additionals by ID (regression in 0.30.0).
    -   The z-Coordinate of junctions is now properly displayed again in inspect mode (regression in 0.30.00).
    -   The z-Coordinate of junctions is no longer reset to 0 when moving them with *move mode*.
    -   busStop and chargingStation elements with negative *startPos* or *endPos* can now be loaded.
    -   Undo now restores the selection status of deleted additionals.
    -   Loading color schemes is now working (only schemes saved by Netedit are valid).
    -   Fixed invalid geo-reference when editing lefthand networks
    -   The cycle time is now always shown for selected traffic lights in tls-mode.
    -   Output precision set in the Options dialog now take effect.
    -   When selecting edges (or lanes) that allow a specific vehicle class, edges (and lanes) with are now matched.
    -   Fixed crash when <ctrl>-clicking on invalid lanes in connection-mode.
    -   Fixed invalid edge shape after setting a custom node shape.
    -   Function *replace by geometry node* now preserves connections, crossings and custom geometry endpoinds. If the function is disabled, the reason is shown in the menu.
    -   Joining junctions now always preserves edge endpoints.
    -   Fixed invalid network after deleting traffic light and a junction with pedestrian crossings.
    -   Fixed crash when joining tls.
    -   The junction visualization option *Show lane to lane connections* now takes effect.

<!-- -->

-   DUAROUTER
    -   Fixed bugs that were causing intermodal routing failures. ,
    -   Fixed invalid output when specifying both and in the input files.
    -   Fixed (almost) infinite loop when specifying without *end*.
    -   Fixed handling of *departPos* and *arrivalPos* for persons.

<!-- -->

-   MAROUTER
    -   Fixed crash due to error in matrix parsing.

<!-- -->

-   TraCI
    -   After sending command *traci.load()* the simulation now keeps running until sending *traci.close()* instead of terminating when there are no more vehicles or the end time is reached.
    -   Vehicle state change retrieval (*simulation.getDepartedIDList, simulation.getArrivedNumber, ...*) are now working after sending command *traci.load()*.
    -   Vehicle commands *getDistance* and *getDrivingDistance* now return correct values when the current vehicle edge or the target edge are junction-internal edges.
    -   Fixed invalid lane occupancy values when calling moveToXY.
    -   *traci.load()* is now working if the previous simulation had errors.
    -   Invalid edge ids in *traci.vehicle.setRoute()* no longer cause crashing.
    -   Fixed *moveToXY* mapping failures.
    -   Person context subscriptions are now working.
    -   Fixed invalid behavior after canceling stop.
    -   Fixed freeze when calling *gui.screenshot*

<!-- -->

-   Tools
    -   [netdiff.py](/Tools/Net#netdiff.py "wikilink") now correctly handles junctions that had their *radius* or *z* attributes changed to the (unwritten) default value.
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") now correctly handles that contain a space in the value (i.e. *modes*).
    -   Fixed bug that was causing insufficient flow when using [flowrouter.py](/Tools/Detector#flowrouter.py "wikilink").
    -   Fixed [flowrouter.py](/Tools/Detector#flowrouter.py "wikilink") crash.

### Enhancements

-   Simulation
    -   Behavior at intersections can now be configured with new [junction model parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Junction_Model_Parameters "wikilink").
    -   Emergency vehicles () may always overtake on the right.
    -   The default car following model can now be specified on the command line with .
    -   Routing with is now working efficiently when using [traffic assignment zones](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Traffic_assignement_zones_.28TAZ.29 "wikilink").
    -   [Lanechange-output](/Simulation/Output/Lanechange "wikilink") now includes the *type* of the changing and the longitudinal gaps on the target lane.
    -   Stops on internal lanes may now be defined.
    -   Aggregate trip information generated via option now includes vehicles that were still running at simulation end if the option is also set.
    -   Vehicles now react to pedestrians on the same lane.
    -   Pedestrians now react to vehicles that are blocking their path.
    -   Collisions between vehicles and pedestrians are now detected when setting the option .
    -   Pedestrian s may now be defined using attribute *route*.
    -   Summary-output now includes mean vehicle speed (absolute and relative) as well as the number of halting vehicles.
    -   Pedestrian statistics are now included in the [aggregated traffic measures](/Simulation/Output#Aggregated_Traffic_Measures "wikilink").
    -   Tripinfo-output now includes additional attributes for persons and containers stages (*depart, waitingTime, duration, vehicle, arrivalPos, actType*).
    -   Added new lanechangeModel parameter *lcAccelLat* to model lateral acceleration in the sublane model.

<!-- -->

-   SUMO-GUI
    -   All values of simulation objects (i.e. TLS) can now be inspected.
    -   Calibrators can now be defined for specific lanes not just for the whole edge.
    -   When using the [Sublane model](/Simulation/SublaneModel "wikilink"), the lateral offset of left and right vehicle side as well as the rightmost and leftmost sublane are listed in the vehicle parameter dialog.
    -   Added button for calibrating lane/edge colors to the current value range.
    -   [POIs](/Simulation/Shapes#POI_.28Point_of_interest.29_Definitions "wikilink") which are defined using attributes *lane* and *pos* now accept the optional attribute *posLat* for specifying lateral offset relative to the lane. . These attributes are automatically added as [generic parameters](/Simulation/GenericParameters "wikilink") retrievable via TraCI.
    -   Added option to configure the aggregation interval of value tracker windows. Previously this was fixed at 1s. Now it defaults to the value.

<!-- -->

-   NETCONVERT
    -   [<split>-definitions](/Networks/Building_Networks_from_own_XML-descriptions#Road_Segment_Refining "wikilink") now support the attribute *id* to specify the id of the newly created node. Two-way roads can be split with the same node by using the same id in two split definitions.
    -   Variable lane widths are now taken into account when importing OpenDrive networks. The new option is used to determine which parts of a lane are not usable by the vehicles (*default 1.8m*).
    -   Added option for building a red phase at traffic lights that do not have a conflicting stream (i.e. roads with a a pedestrian crossing in a network that is not meant for pedestrian simulation). The new default value is 5 seconds.
    -   Added option for building all-red phases after every yellow phase.
    -   Added option to allow [generation of walkingareas](/Simulation/Pedestrians#walkingareas "wikilink") in networks without pedestrian crossings.
    -   Added option to ensure that opposite lane information can be set for curved roads. (see [Simulation/OppositeDirectionDriving\#Limitations](/Simulation/OppositeDirectionDriving#Limitations "wikilink")).
    -   Custom lane shapes [can now be defined](/Networks/Building_Networks_from_own_XML-descriptions#Lane-specific_Definitions "wikilink").
    -   Added options and for defining the time range of non-static traffic lights.
    -   The option now accepts arbitrary floats and can be used to scale the output network.

<!-- -->

-   NETEDIT
    -   [POIs and Polygons](/NETEDIT#POIs_and_Polygons "wikilink") can now be defined with a new editing mode.
    -   Minimum and maximum phase duration for actuated traffic lights can now be defined.
    -   Added button for calibrating lane/edge colors to the current value range.

<!-- -->

-   TraCI
    -   Support for multiple clients.
    -   Added function *vehicle.getAccumulatedWaitingTime* to retrieve the waiting time collected over the interval .
    -   Added many value retrieval functions to the C++ client. Thanks to Raphael Riebl for the patch!
    -   New vehicle types can be created dynamically (by duplicating existent). -&gt; *traci.vehicletype.copy()*
    -   Added function *person.rerouteTraveltime* to [reroute pedestrians](/TraCI/Change_Person_State#Command_0xce:_Change_Person_State "wikilink").
    -   Rerouting-device [period can now be set for individual vehicles. assumed edge travel times can be set globally.](/TraCI/Change_Vehicle_State#Supported_Device_Parameters "wikilink")
    -   Rerouting-device [period and assumed edge travel times can now be retrieved.](/TraCI/Vehicle_Value_Retrieval#Supported_Device_Parameters "wikilink")

<!-- -->

-   DUAROUTER
    -   Routing with is now working efficiently when using [traffic assignment zones](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Traffic_assignement_zones_.28TAZ.29 "wikilink").
    -   Stops on internal lanes are now supported.
    -   Pedestrian s may now be defined using attribute *route*.

<!-- -->

-   DFROUTER
    -   Added option for randomizing the departure times of generated vehicles.

<!-- -->

-   OD2TRIPS
    -   Added option for generating pedestrian demand rather than vehicles.
    -   Added option for generating [intermodal traffic demand](/Specification/Persons#PersonTrips "wikilink").

<!-- -->

-   Tools
    -   [osmWebWizard.py](/Tools/Import/OSM#osmWebWizard.py "wikilink") now supports location search.
    -   [osmWebWizard.py](/Tools/Import/OSM#osmWebWizard.py "wikilink") now generates scenarios with actuated traffic lights
    -   [osmWebWizard.py](/Tools/Import/OSM#osmWebWizard.py "wikilink") now generates traffic with more realistic speed distribution
    -   flowrouter.py now supports [specifying route restrictions to resolve ambiguities](/Tools/Detector#Ambiguity "wikilink").
    -   When setting [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") option , vType attributes from option are recognized and writen to the generated vType.

### Other

-   SUMO now uses C++11
-   specifying the car following model as nested element in a vType is now deprecated
-   trips without ids are deprecated
-   router options are now more consistent with simulation options
    -   use -a for additional files
    -   use -r or --route-files for all kinds of route input (trips, flows, routes, alternatives)
    -   the old options --flows, --trips, -- alternatives are deprecated
    -   The network argument for [routeStats.py](/Tools/Routes#routeStats.py "wikilink") is now optional and set with option .
-   The option which used to be an alias for is no longer supported. These option were used to set a scaling factor by negative powers of ten but now sets the scaling factor directly (the previous value **5** now corresponds to **1e-5**)
-   default *detector-gap* for [actuated traffic lights](/Simulation/Traffic_Lights#Based_on_Time_Gaps "wikilink") is now 2.0s.
-   default *minGapLat* value (used by the [sublane model](/Simulation/SublaneModel "wikilink") is now 0.6m (down from 1.0m) to better match observations.
-   Documentation
    -   Added description of [automatically generated traffic light programs](/Simulation/Traffic_Lights#Automatically_Generated_TLS-Programs "wikilink").
    -   Added Tutorial for [importing public transport data from OSM](/Tutorials/PT_from_OpenStreetMap "wikilink").
    -   Extended page on [Safety-related topics](/Simulation/Safety "wikilink")
    -   Added overview page for [Geo-Coordinates](/Geo-Coordinates "wikilink")
-   TraCI
    -   TraCI version is now 16

Older Versions
--------------

-   [z/Changes from Version 0.29.0 to Version 0.30.0](/z/Changes_from_Version_0.29.0_to_Version_0.30.0 "wikilink")
-   [z/Changes from Version 0.28.0 to Version 0.29.0](/z/Changes_from_Version_0.28.0_to_Version_0.29.0 "wikilink")
-   [z/Changes from Version 0.27.1 to Version 0.28.0](/z/Changes_from_Version_0.27.1_to_Version_0.28.0 "wikilink")
-   [z/Changes from Version 0.27.0 to Version 0.27.1](/z/Changes_from_Version_0.27.0_to_Version_0.27.1 "wikilink")
-   [z/Changes from Version 0.26.0 to Version 0.27.0](/z/Changes_from_Version_0.26.0_to_Version_0.27.0 "wikilink")
-   [z/Changes from Version 0.25.0 to Version 0.26.0](/z/Changes_from_Version_0.25.0_to_Version_0.26.0 "wikilink")
-   [z/Changes from Version 0.24.0 to Version 0.25.0](/z/Changes_from_Version_0.24.0_to_Version_0.25.0 "wikilink")
-   [z/Changes from Version 0.23.0 to Version 0.24.0](/z/Changes_from_Version_0.23.0_to_Version_0.24.0 "wikilink")
-   [z/Changes from Version 0.22.0 to Version 0.23.0](/z/Changes_from_Version_0.22.0_to_Version_0.23.0 "wikilink")
-   [z/Changes from Version 0.21.0 to Version 0.22.0](/z/Changes_from_Version_0.21.0_to_Version_0.22.0 "wikilink")
-   [z/Changes from Version 0.20.0 to Version 0.21.0](/z/Changes_from_Version_0.20.0_to_Version_0.21.0 "wikilink")
-   [z/Changes from Version 0.19.0 to Version 0.20.0](/z/Changes_from_Version_0.19.0_to_Version_0.20.0 "wikilink")
-   [z/Changes from Version 0.18.0 to Version 0.19.0](/z/Changes_from_Version_0.18.0_to_Version_0.19.0 "wikilink")
-   [z/Changes from Version 0.17.1 to Version 0.18.0](/z/Changes_from_Version_0.17.1_to_Version_0.18.0 "wikilink")
-   [z/Changes from Version 0.17.0 to Version 0.17.1](/z/Changes_from_Version_0.17.0_to_Version_0.17.1 "wikilink")
-   [z/Changes from Version 0.16.0 to Version 0.17.0](/z/Changes_from_Version_0.16.0_to_Version_0.17.0 "wikilink")
-   [z/Changes from Version 0.15.0 to Version 0.16.0](/z/Changes_from_Version_0.15.0_to_Version_0.16.0 "wikilink")
-   [z/Changes from Version 0.14.0 to Version 0.15.0](/z/Changes_from_Version_0.14.0_to_Version_0.15.0 "wikilink")
-   [z/Changes from Version 0.13.1 to Version 0.14.0](/z/Changes_from_Version_0.13.1_to_Version_0.14.0 "wikilink")
-   [z/Changes from Version 0.13.0 to Version 0.13.1](/z/Changes_from_Version_0.13.0_to_Version_0.13.1 "wikilink")
-   [z/Changes from Version 0.12.3 to Version 0.13.0](/z/Changes_from_Version_0.12.3_to_Version_0.13.0 "wikilink")
-   [z/Changes from Version 0.12.2 to Version 0.12.3](/z/Changes_from_Version_0.12.2_to_Version_0.12.3 "wikilink")
-   [z/Changes from Version 0.12.1 to Version 0.12.2](/z/Changes_from_Version_0.12.1_to_Version_0.12.2 "wikilink")
-   [z/Changes from Version 0.12.0 to Version 0.12.1](/z/Changes_from_Version_0.12.0_to_Version_0.12.1 "wikilink")
-   [z/Changes from Version 0.11.1 to Version 0.12.0](/z/Changes_from_Version_0.11.1_to_Version_0.12.0 "wikilink")
-   [z/Changes from Version 0.11.0 to Version 0.11.1](/z/Changes_from_Version_0.11.0_to_Version_0.11.1 "wikilink")
-   [z/Changes from Version 0.10.3 to Version 0.11.0](/z/Changes_from_Version_0.10.3_to_Version_0.11.0 "wikilink")
-   [z/Changes from Version 0.10.2 to Version 0.10.3](/z/Changes_from_Version_0.10.2_to_Version_0.10.3 "wikilink")
-   [z/Changes from Version 0.10.1 to Version 0.10.2](/z/Changes_from_Version_0.10.1_to_Version_0.10.2 "wikilink")
-   [z/Changes from Version 0.10.0 to Version 0.10.1](/z/Changes_from_Version_0.10.0_to_Version_0.10.1 "wikilink")
-   [z/Changes from Version 0.9.10 to Version 0.10.0](/z/Changes_from_Version_0.9.10_to_Version_0.10.0 "wikilink")
-   [z/Changes from version 0.9.9 to version 0.9.10](/z/Changes_from_version_0.9.9_to_version_0.9.10 "wikilink")
-   [z/Changes from version 0.9.8 to version 0.9.9](/z/Changes_from_version_0.9.8_to_version_0.9.9 "wikilink")
-   [z/Changes from version 0.9.7 to version 0.9.8](/z/Changes_from_version_0.9.7_to_version_0.9.8 "wikilink")
-   [z/Changes from version 0.9.6 to version 0.9.7](/z/Changes_from_version_0.9.6_to_version_0.9.7 "wikilink")
-   [z/Changes from version 0.9.5 to version 0.9.6](/z/Changes_from_version_0.9.5_to_version_0.9.6 "wikilink")
-   [z/Changes from version 0.9.3 to version 0.9.4](/z/Changes_from_version_0.9.3_to_version_0.9.4 "wikilink")
-   [z/Changes from version 0.9.2 to version 0.9.3](/z/Changes_from_version_0.9.2_to_version_0.9.3 "wikilink")
-   [z/Changes from version 0.9.1 to version 0.9.2](/z/Changes_from_version_0.9.1_to_version_0.9.2 "wikilink")
-   [z/Changes from version 0.9.0 to version 0.9.1](/z/Changes_from_version_0.9.0_to_version_0.9.1 "wikilink")
-   [z/Changes from version 0.8.x to version 0.9.0](/z/Changes_from_version_0.8.x_to_version_0.9.0 "wikilink")
-   [z/Changes from version 0.8.2.2 to version 0.8.3](/z/Changes_from_version_0.8.2.2_to_version_0.8.3 "wikilink")
-   [z/Changes from version 0.8.2.1 to version 0.8.2.2](/z/Changes_from_version_0.8.2.1_to_version_0.8.2.2 "wikilink")
-   [z/Changes from version 0.8.0.2 to version 0.8.2.1](/z/Changes_from_version_0.8.0.2_to_version_0.8.2.1 "wikilink")
-   [z/Changes from version 0.8.0.1 to version 0.8.0.2](/z/Changes_from_version_0.8.0.1_to_version_0.8.0.2 "wikilink")
-   [z/Changes from version 0.8.0 to version 0.8.0.1](/z/Changes_from_version_0.8.0_to_version_0.8.0.1 "wikilink")
-   [z/Changes from version 0.7.0 to version pre0.8](/z/Changes_from_version_0.7.0_to_version_pre0.8 "wikilink")
