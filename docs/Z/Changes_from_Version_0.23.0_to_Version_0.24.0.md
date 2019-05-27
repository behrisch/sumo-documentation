---
title: Z Changes from Version 0.23.0 to Version 0.24.0
permalink: /Z/Changes_from_Version_0.23.0_to_Version_0.24.0/
---

Version 0.24.0 (02.09.2015)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed default arrivalPos when loading or elements using attributes directly into SUMO.
    -   Fixed crash when specifying consecutive walks for the same person.
    -   Fixed bug that caused pedestrians to get too close to each other.
    -   Fixed crash and other bugs when using option . , , ,
    -   Fixed bug that sometimes caused the rear end of vehicles to be placed on the wrong lane after lane-changing.
    -   Rerouters where closed edges are disabled for specific vehicle classes now cause these vehicles to wait until the closing ends if the destination edge is closed.
    -   Vehicles with a in their route are now being overtaken if there is sufficient space. This was causing problems when modelling parked vehicles on a multi-lane road.
    -   Fixed bug that resulted in invalid routes when routing at simulation time (at intersections where a required connection originates from a prohibited lane).
-   SUMO-GUI
    -   Fixed centering of names on objects (a large mismatch was visible for persons).
    -   Polygons are no longer drawn when setting their size-exaggeration to 0.
-   DUAROUTER
    -   Custom car following model specification is now preserved in the route output.
    -   Fixed bug when using option where the start/destination edge changed needlessly.
    -   Vehicles may now depart/arrive at any *TAZ* regardless of their vehicle class.
-   NETCONVERT
    -   When adding crossings to a *.net.xml* without internal links, the output network will be built with internal links. .
    -   Fixed bug where duplicate crossings between the same pair of walkingareas where sometimes build when using option .
    -   Fixed bugs where loading a *.net.xml* file and removing edges would lead to an invalid network. ,,
    -   Permissions are no longer lost when guessing ramps.
    -   Defining pedestrian crossings at a node with now works.
    -   Fixed invalid TLS-plans when loading a *.net.xml* file with TLS-controlled pedestrian crossings.
    -   Connections between lanes with incompatible vehicle classes are no longer generated.
    -   Fixed generation of connections at intersections with dedicated bicycle lanes (symptoms were invalid connections and missing connections).
    -   Modifying lane permissions in a network with crossings, so that crossings are no longer valid, is now working (invalid crossings are removed with a warning).
    -   Fixed bug that caused invalid lane lengths when building with option (near intersections with sharp angles).
    -   Fixed some invalid clusters when using option .
-   TraCI
    -   Fixed python API for [function *move to VTD* (0xb4)](/TraCI/Change_Vehicle_State# "wikilink").
    -   Fixed subscriptions for
    -   Vehicle command *move to* (0x5c) can now be used to forcefully insert vehicles which have not yet entered the network.
    -   Parking vehicles now return a reasonable position (and other values which do not depend on being on a lane).
    -   Fixed screenshots for Linux.
    -   The close command returns now a little later to have more data written to files (still not completely flushed though, see )
-   NETEDIT
    -   Fixed bug where unselected objects were wrongly selected after undoing deletion.
    -   No longer creating invalid network when loading and saving a network with split crossings.
-   Tools
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") no longer attempts to find a fringe based on edge-direction when using option .
-   All Applications
    -   Fixed invalid paths when using option and loading a configuration file in a subdirectory.

### Enhancements

-   Simulation
    -   Simulation of [electric vehicles is now supported](/Models/Electric "wikilink") with a new model for energy consumption and battery charging.
    -   Maximum time that may be simulated increased from 24 days to 290 million years.
    -   [-definitions](/Specification/Persons#Walking "wikilink") now support and .
    -   now includes z-data if the network has elevation.

    -   [](/Simulation/Output/VTypeProbe "wikilink") output now includes z-data if the network has elevation.
    -   Device [assignment by ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Devices "wikilink") can now be used to override device assignment by option .
    -   Added new -attribute which can be used instead of a child element when declearing the car following model.
    -   Vehicles which do not have a route and cannot find one on insertion get discarded when is given.
    -   now includes the route length.

-   SUMO-GUI
    -   The view can now be moved and zoomed via [keyboard shortcuts](/SUMO-GUI#Keyboard_Shortcuts "wikilink").
    -   Lanes which disallow passenger cars (i.e. paths and service roads) now have a distinct shade of grey. The color can be customized in the gui-settings dialog.
    -   Vehicles now activate their blinker during continuous lane change manoeuvres.
    -   The types of POIs and Polygons can now be displayed via *View Settings*.
    -   The information for a vehicle is now shown in the parameter dialog.
    -   The GUI asks at simulation end whether all files and windows should be closed
-   NETCONVERT
    -   added option which works as an analogue to . Giving either option a selection file (where edge ids are prefixed with **edge:** as argument is now supported.
    -   added option which works as an analogue to and prevents edges from being treated as on- or off-ramps.
    -   Now importing signalized pedestrian crossings from [OSM](/Networks/Import/OpenStreetMap "wikilink") ().
    -   added new option and new attributes [for allowing drivers to drive onto an intersection despite the risk of blocking it for cross-traffic](/Simulation/Intersections#NETCONVERT_options_for_allowing_drivers_to_drive_onto_intersections "wikilink").
    -   pedestrian crossings may be removed using the [new attribute ](/Networks/Building_Networks_from_own_XML-descriptions#Pedestrian_Crossings "wikilink").
    -   when splitting an edge, the new node is not removed by option even when speed and lane count remain unchanged.
    -   Connections from and to sidewalks are only generated when also building pedestrian crossings since they are superfluous otherwise. When using pedestrian model *nonInteracting* these connections are not used (pedestrians *jump* across intersections between any two sidewalks) and when using model *striping*, crossings are mandatory.
    -   Bicycle lanes are now imported from [OSM (when using the appropriate typemap)](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink").
    -   Bus lanes are now imported from [OSM](/Networks/Import/OpenStreetMap "wikilink").
    -   Improved control over edge types (typemaps) when importing from [OSM](/Networks/Import/OpenStreetMap "wikilink"). All defaults can now be overridden in a transparent manner and it's easier to add additional modes of traffic than ever before [(see documentation)](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink").
    -   Option now works for generating networks with left-hand traffic. Thansk to Andrea Fuksova for suggesting the double-mirroring technique.
    -   Edge types can now be used to [define *vClass*-specific speed limits](/Networks/Building_Networks_from_own_XML-descriptions#vehicle-class_specific_speed_limits "wikilink").
    -   Additional attributes are now supported to specify the node that is generated when [splitting an edge](/Networks/Building_Networks_from_own_XML-descriptions#Road_Segment_Refining "wikilink").
-   DUAROUTER
    -   option now also applies if no input trips/routes are loaded.
    -   Added option to improve routing speed when many (similar) vehicles depart at the same time from the same location. The time aggregation can be controlled using option The *bulkstar* routing algorithm is now obsolete and no longer supported.
    -   Added options , which attempts to repair invalid source or destination edges in the route input.
-   TraCI
    -   added [command to retrieve persons on an edge](/TraCI/Edge_Value_Retrieval "wikilink"). Also added the corresponding method *traci.edge.getLastStepPersonIDs()* to the [python API](/TraCI/Interfacing_TraCI_from_Python "wikilink").
    -   added method *traci.vehicle.getStopState()* to the [python API](/TraCI/Interfacing_TraCI_from_Python "wikilink") [(command 0xb5)](/TraCI/Vehicle_Value_Retrieval "wikilink"). Also added convenience methods *traci.vehicle.isStopped(), traci.vehicle.isStoppedParking, traci.vehicle.isStoppedTriggered()*.
    -   added [command to retrieve the next edge of a walking person](/TraCI/Person_Value_Retrieval "wikilink"). Also added the corresponding method *traci.person.getNextEdge()* to the [python API](/TraCI/Interfacing_TraCI_from_Python "wikilink"). This can be used to implement pedestrian-actuated traffic lights.
    -   Added named constant *traci.vehicle.DEPART_SPEED_RANDOM*. This corresponds to .
    -   Added variable retrieval functions for [](/TraCI/Lane_Area_Detector_Value_Retrieval "wikilink"): lane, position, and length. Also added corresponding functions to the [python API](/TraCI/Interfacing_TraCI_from_Python "wikilink")
    -   added [command to retrieve the index of the vehicles edge within it's route](/TraCI/Vehicle_Value_Retrieval "wikilink"). Also added the corresponding method *traci.vehicle.getRouteIndex()* to the [python API](/TraCI/Interfacing_TraCI_from_Python "wikilink").
    -   extended method *traci.vehicle.setStop(...)* to optionally include the startPos of a stop.
-   POLYCONVERT
    -   When importing OSM data, POIs are now raised above the layer of polygons and roads by default to make them always visible.
    -   Added option to control the layer of pois relative to polygons (especially in cases where they have the same type).
    -   options are now respeced even when used together with a network.

-   NETEDIT
    -   The view can now be moved and zoomed via [keyboard shortcuts](/SUMO-GUI#Keyboard_Shortcuts "wikilink").
    -   Added menu option for replacing junctions by geometry points.
    -   Geometry points of parallel edges can now be moved simultaneously when both edges are selected.
    -   option is now supported.
-   OD2TRIPS
    -   can now choose only differing sources and sinks

<!-- -->

-   Tools
    -   made edgesInDistricts.py aware of vClasses (and use the sumolib for parsing)
    -   added [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") option for achieving binomially distributed arrival rates.
    -   added [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") option for generating trips with validated connectivity.
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") now supports attributes for and definitions when using option .
    -   [netcheck.py](/Tools/Net#netcheck.py "wikilink") now supports discovering reverse connectivity by using option
    -   [netcheck.py](/Tools/Net#netcheck.py "wikilink") now supports edge permissions by using option
    -   [netcheck.py](/Tools/Net#netcheck.py "wikilink") now supports writing an edge selecting for every (weakly) connected component when using option
    -   [netcheck.py](/Tools/Net#netcheck.py "wikilink") now outputs additional statistics in regard to the disconnected components. Thanks to Gregory Albiston for the patch.
    -   added new tool [districts2poly.py](/Tools/District#districts2poly.py "wikilink") for visualizing districts.
    -   added new tool [route2sel.py](/Tools/Routes#route2sel.py "wikilink") for creating an edge selection from a route file.
    -   added new tool [edgeDataDiff.py](/Tools/Output#edgeDataDiff.py "wikilink") for comparing two traffic scenarios via their [edgeData output](/Simulation/Output/Lane-_or_Edge-based_Traffic_Measures "wikilink").
    -   [tls_csv2SUMO.py](/Tools/tls "wikilink") now supports multiple definitions in a single input file. Thanks to Thomas Lockhart for the patch.
    -   OSM-scenario-generator script [server.py](/Tools/Import/OSM "wikilink") now supports additional modes of traffic.
    -   *traceExporter.py* now supports filtering to a bounding box.

### Other

-   Scenarios
    -   An updated version of the [TAPASCologne scenario](/Data/Scenarios/TAPASCologne "wikilink") can be found on [the sourceforge download page](http://sourceforge.net/projects/sumo/files/traffic_data/scenarios/TAPASCologne). This updates the network to the latest OSM data and [NETCONVERT](/NETCONVERT "wikilink") version.
    -   An updated version of the [Bologna scenarios](/Data/Scenarios#Bologna "wikilink") can be found on [the sourceforge download page](https://sourceforge.net/projects/sumo/files/traffic_data/scenarios/Bologna_small/). This contains minor network fixes and contains a new pedestrian version of the *acosta*-scenario
-   Documentation
    -   Added new tutorial [Tutorials/TraCIPedCrossing](/Tutorials/TraCIPedCrossing "wikilink") which shows how to build a pedestrian-actuated traffic light controller.
    -   Documented [TraCI function *move to VTD* (0xb4)](/TraCI/Change_Vehicle_State# "wikilink")
    -   cleaned XML schema concerning person capacity and person number definition
    -   Documented [tllogic files](/Networks/Building_Networks_from_own_XML-descriptions#Traffic_Light_Program_Definition "wikilink")
    -   Documented current state of [bicycle simulation](/Simulation/Bicycles "wikilink"), [train simulation](/Simulation/Railways "wikilink") and [waterway simulation](/Simulation/Waterways "wikilink").
    -   Added description of [intersection dynamics](/Simulation/Intersections "wikilink").
-   TraCI
    -   TraCI version is now 10
    -   The named constant *traci.vehicle.DEPART_MAX* is now named *traci.vehicle.DEPART_SPEED_MAX*. This corresponds to .
-   Tools
    -   GDAL 2.0 is now supported. Thanks to Thomas Lockhart for the patch.
    -   osmBuild.py and [server.py](/Tools/Import/OSM "wikilink") no longer use option to avoid removing rivers and railways.
-   Misc
    -   The scripts *randomTrips.py* and *route2trips.py* moved from <SUMO_HOME>/tools/trip to <SUMO_HOME>/tools
    -   The [OSM typemaps](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink") now disallow vClass *tram* and *ship* where appropriate
    -   The tool *sumoplayer* has been removed because it became obsolete with the introduction of and *traceExporter.py*.
    -   The Win64 binaries no longer have a 64 suffix.
    -   Error reporting on opening files got a little more verbose.
    -   Whitespace in filenames is handled a little bit better
