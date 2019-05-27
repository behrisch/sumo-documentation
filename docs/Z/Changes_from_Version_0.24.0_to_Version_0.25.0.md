---
title: Z Changes from Version 0.24.0 to Version 0.25.0
permalink: /Z/Changes_from_Version_0.24.0_to_Version_0.25.0/
---

Version 0.25.0 (07.12.2015)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed crashing and deadlocks when performing [routing in the simulation based](/Demand/Automatic_Routing "wikilink") on [districts](/Demand/Importing_O/D_Matrices#Describing_the_TAZ "wikilink").
    -   Fixed bug that was hindering lane-changes due to invalid cooperative speed adaptations.
    -   Fixed bug that was causing erratic lane changes when using subsecond simulation.
    -   Fixed bug that was causing erratic lane changes in front of intersections.
    -   Fixed right-of-way in regard to vehicles that were driving across the same intersection twice.
    -   Vehicles waiting to enter a roundabout no longer yield to other vehicles outside the roundabout.
    -   Pedestrians no longer walk past their specified arrival position.
    -   Fixed asymmetrical pedestrian behavior when walking to a *busStop*. Now they always walk to the middle of the busstop rather than to its *endPos*.

<!-- -->

-   SUMO-GUI
    -   Fixing crash when selecting *Show all routes* from the vehicle menu.
    -   When loading a gui-settings-file from the *View Settings* dialog, the delay value is now correctly applied.
    -   Fix bug that caused giant circles to appear when exaggerating the width of lanes with short geometry segments.
    -   Vehicle names are now drawn for vehicles that occupy multiple edges.
    -   Fixed drawing of link indices, link rules, lane markings and bus stops for left-hand networks.
    -   Fixed error when reloading a network with -elements.

<!-- -->

-   NETCONVERT
    -   Fixed missing connections in multi-modal networks.
    -   Fixed bug that caused invalid pedestrian crossings to be generated after importing a *.net.xml* file.
    -   Fixed bug that caused pedestrian crossings to change their priority when importing a *.net.xml* file.
    -   Fixed geometry bug when building pedestrian crossings and walkingareas for left-hand networks.
    -   Fixed invalid network after deleting edges at a joined traffic light with controlled pedestrian crossing.
    -   Motorway ramps are no longer guessed if the lane permissions indicate that the edge is not a motorway.
    -   Motorway ramps are no longer guessed at roundabouts.
    -   Fixed some cases when roads where invalidly guessed to be roundabouts.
    -   When importing a *.net.xml* file the resulting network is no longer modified due to automatic joining of edges that connect the same nodes.
    -   When importing a *.net.xml* file with pedestrian crossings and setting option , the crossings and walkingareas are removed from the resulting network.
    -   Several fixes in regard to OpenDrive networks:
        -   Fixed missing elements when exporting networks as [OpenDrive](/Networks/Import/OpenDRIVE "wikilink").
        -   Now successfully importing [OpenDrive networks](/Networks/Import/OpenDRIVE "wikilink") with dead-end edges.
        -   Fixed imprecise geometry when importing [OpenDrive](/Networks/Import/OpenDRIVE "wikilink") networks.
        -   Fixed imprecise geometry when exporting networks as [OpenDrive](/Networks/Import/OpenDRIVE "wikilink").
        -   Fixed invalid geometry of lanes within intersections when exporting networks as [OpenDrive](/Networks/Import/OpenDRIVE "wikilink").
    -   Fixed crash when specifying inconsistent [tllogic input](/Networks/Building_Networks_from_own_XML-descriptions#Traffic_Light_Program_Definition "wikilink").
    -   When patching an existing network with *.nod.xml* file, existing traffic light programs are now preserved unless changes are specified explicitly.
    -   No longer patching loaded traffic light programs for new crossings if they already have the correct state size.
    -   When importing a *.net.xml* which was built for left-hand traffic, the resulting network will also be built for left-hand traffic.
    -   When importing a *.net.xml*, generated networks will retain the same value of ) as the input network.
    -   Fixed invalid geo-referencing in left-hand networks.
    -   Traffic lights that control multiple intersections no longer create unsafe right-of-way rules. The edges that lie within the traffic light are now controlled according to the appropriate right of way (This does not necessarily model physical traffic signals but reflects the behavior of drivers).
        -   Old signal plans for these *joined* traffic lights no longer work for new networks since more link states need to be defined. The option was added to build networks that are compatible with old-style signal plans. Note, that this may create unsafe intersections, causing collisions.

<!-- -->

-   NETEDIT
    -   When renaming an edge, the lane IDs are now updated as well.
    -   Fractional widths can now be set when inspecting edges.
    -   Modifying traffic light plans which control multiple nodes is now working.

<!-- -->

-   DUAROUTER
    -   Fixed invalid error when compiled without the FOX library.

<!-- -->

-   OD2TRIPS
    -   Option is now working.

<!-- -->

-   MESO-GUI
    -   Loading of edge-scaling schemes from a *gui-settings-file* is now working.
    -   The front of each vehicle queue is now drawn at the start of its segment.

<!-- -->

-   TraCI
    -   Fixed bug that prevented the [C++ TraCI library](/TraCI/C%2B%2BTraCIAPI "wikilink") from functioning.
    -   [Vehicle command](/TraCI/Change_Vehicle_State "wikilink") *set speed* can now be used in conjunction with *move to VTD*.
    -   When using [Vehicle command](/TraCI/Change_Vehicle_State "wikilink") *move to VTD*, the speed is set according to the covered distance where this is deemed plausible (the value of *set speed* overrides this).

<!-- -->

-   Tools
    -   [osmWebWizard.py](/Tools/Import/OSM "wikilink") no longer fails when encountering path names with space-charactes in them.
    -   [osmWebWizard.py](/Tools/Import/OSM "wikilink") no longer nests output directories when generating multiple scenarios.

### Enhancements

-   Simulation
    -   [Vehicle types](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") now have by default. Earlier, the default was which would let the vehicles drive along footpaths and railways.
    -   [Zipper merging](https://en.wikipedia.org/wiki/Merge_%28traffic%29) is now supported (see Netconvert enhancement below).
    -   Added person statistics to [verbose output](/Simulation/Output#Commandline_Output_.28verbose.29 "wikilink").
    -   Now warning about jammed pedestrians.
    -   Now warning about pedestrians “collisions”.
    -   Now warning about traffic lights where one link never gets a green light.
    -   It is now possible to [modify the offset of an existing tls program](/Simulation/Traffic_Lights#Modifying_Existing_TLS-Programs "wikilink") without loading a completely new -definition.
    -   Added option which causes average vehicle trip data to be [printed in verbose mode](/Simulation/Output#Commandline_Output_.28verbose.29 "wikilink") (average route length, travel time and time loss, ...) for quick evaluation of a scenario.
    -   The option can now be used to maintain a constant number of vehicles in the network. Vehicle insertions are delayed whenever this number would be exceeded. Previously this option would terminate the simulation when the number was exceeded. To avoid a large number of delayed vehicles it is recommended to use the option .
    -   Traffic detectors which are generated for [actuated traffic lights now support additional parameters](/Simulation/Traffic_Lights#Actuated_Traffic_Lights "wikilink") to allow writing output files the same way as [regular detectors](/Simulation/Output/Induction_Loops_Detectors_(E1) "wikilink").
    -   Angles in simulation output and TraCI results now conform to *Navigational Standards* with *0* pointing towards the North and *90* pointing due East.

<!-- -->

-   NETEDIT
    -   [NETEDIT](/NETEDIT "wikilink") is now open. Have fun.
    -   Int and float options can now be set in the *Processing-&gt;Options* dialog.
    -   Added many lane- and junction-coloring modes already known from [SUMO-GUI](/SUMO-GUI#Edge.2FLane_Visualisation_Settings "wikilink").
    -   Pedestrian crossings are now supported when editing traffic light plans.
    -   Attributes of pedestrian crossings can now be modified.
    -   Added context-menu option for removing intermediate geometry points from selected edges.
    -   Vehicle class permissions can now be edited via check-boxes instead of typing all class names.
    -   Individual lanes and selections of lanes can now be deleted when unchecking *Select edges*.
    -   A lane (or a selections of lanes) can now be duplicated by selecting *Duplicate lane* from the context menu.
    -   *Selection Mode* now allows [additional operators](/NETEDIT#Select "wikilink") when matching against a non-numerical attribute.
    -   Added new option *Copy edge name to clipboard* to the lane popup-menu.
    -   Junction attribute *keepClear* is now supported.
    -   Custom junction shapes can now be drawn by selecting *Set custom shape* from the junction popup-menu. This will create a [modifiable shape outline. The popup-menu of this outline allows saving, discarding and simplifying the shape.](/NETEDIT#Modifiable_Poly "wikilink")
    -   Added *reload* menu option.
    -   When editing traffic light plans, [states can now be set for multiple links and multiple phases at the same time](/NETEDIT#Traffic_Lights "wikilink").

<!-- -->

-   SUMO-GUI
    -   Persons can now be tracked by selecting *Start Tracking* from the context menu.
    -   The current route of pedestrians can now be shown by selecting *Show Current Route* from the context menu.
    -   Error messages can now by clicked for jumping to the referenced simulation object (i.e. a teleporting vehicle).
    -   Added person statistics to network parameter dialog.
    -   Added new menu option *Edit-&gt;Open in Netedit* for opening the current network (at the current location) in [NETEDIT](/NETEDIT "wikilink").
    -   Added new option *Copy edge name to clipboard* to the lane popup-menu.
    -   Added new options *Close edge* and *Close lane* to the lane popup-menu. This will force vehicles (with an assigned vClass) to wait until the corresponding lanes have been reopened (also via popup-menu).
    -   Added new option *Add rerouter* to the lane popup-menu. This will make vehicles recompute their route when entering that edge.
    -   The size and color of link indices can now be customized (old [gui settings files](/SUMO-GUI#Changing_the_appearance.2Fvisualisation_of_the_simulation "wikilink") may have to be updated).
    -   Average trip data (for completed vehicle trips) is now available in the network parameter dialogue when running with option .
    -   Added new junction visualization option *draw crossings/walkingareas*.
    -   Vehicles can now be colored *by depart delay* (the differences between desired and actual depart time). Depart delay was also added to the vehicle parameter dialog.
    -   Junction shapes are no longer drawn when their color is set to fully transparent.
    -   The network version is now shown the the network parameter dialog.

<!-- -->

-   NETCONVERT
    -   [Zipper merging](https://en.wikipedia.org/wiki/Merge_%28traffic%29) is now supported via the new [node type *zipper*](/Networks/Building_Networks_from_own_XML-descriptions#Node_types "wikilink").
    -   [Right-turn-on-red](https://en.wikipedia.org/wiki/Right_turn_on_red) is now supported via the new [node type *traffic_light_right_on_red*](/Networks/Building_Networks_from_own_XML-descriptions#Node_types "wikilink").
    -   Importing *.inpx* [VISSIM networks](/Networks/Import/Vissim "wikilink") is now supported. Thanks to the [AIT](http://www.ait.ac.at/) for their contribution.
    -   The positioning and presence of [internal junctions](/Networks/SUMO_Road_Networks#Internal_Junctions "wikilink") can now be [customized with the new connection attribute ](/Networks/Building_Networks_from_own_XML-descriptions#Explicitly_setting_which_Edge_.2F_Lane_is_connected_to_which "wikilink").
    -   The maximum number of connections per junction was raised from 64 to 256.
    -   Added options and to exclude edges from being modified when using option .
    -   When specifying [multiple connections from the same edge to the same target lane](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink"), safe right-of-way rules are now established among the conflicting connections.
    -   Added options to ensure that heuristically generated traffic light plans have a fixed cycle length. The new default is *90* (s) which will have no effect on most 4-arm intersections but will cause different timings for controlled 3-arm intersections and other types.
    -   Added options to select whether edges that connect the same nodes (and have similar geometry) shall be joined into an edge with multiple lanes. The new default is *false* (before, this heuristic was always active).
    -   Street names are now imported form [OpenDrive](/Networks/Import/OpenDRIVE "wikilink").
    -   Now including sumo edge-ids in [OpenDrive export](/Networks/Further_Outputs#OpenDRIVE_Road_Networks "wikilink") if option is given (as ).
    -   Now using more lane types in [OpenDrive export](/Networks/Further_Outputs#OpenDRIVE_Road_Networks "wikilink").
    -   Added option for setting the default of [nodes](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink").
    -   Added option to configure the default duration for the dedicated left-turn phase. A value of 0 disables building this phase.
    -   Added option to prevent guessing a sidewalk for the given list of edges.
    -   Added option for setting the number of geometry points for lanes within intersections (Before, this was hard-coded as *5*).
    -   Added option . This allows setting the speed threshold above which crossings will not be generated at uncontrolled nodes (before this was hard-coded to *13.89*m/s).

<!-- -->

-   POLYCONVERT
    -   Added option to control whether polygons are filled by default or not.
    -   Added option to override the fill state when importing shapefiles. Allowed values are **\[auto|true|false\]**.

<!-- -->

-   MESO-GUI
    -   It is now possible to select individual vehicles, to examine their parameters, track them and show their route just like for [SUMO-GUI](/SUMO-GUI "wikilink").
    -   Vehicles can now be located as in [SUMO-GUI](/SUMO-GUI "wikilink").

<!-- -->

-   Tools
    -   [traceExporter.py](/Tools/TraceExporter "wikilink") now supports exporting traces of persons when using the new option .
    -   Added option for [traceExporter.py](/Tools/TraceExporter "wikilink"). When this is set vehicles will not be destroyed until the end of the fcd-file even when disappearing for a few simulation steps..
    -   The [osmWebWizard.py](/Tools/Import/OSM#server.py "wikilink") import script is now more robust in finding a suitable output directory and recovering from errors.
    -   Added new tool [tlsCoordinator.py](/Tools/tls#tlsCoordinator.py "wikilink") which coordinates traffic lights in a network for a given traffic demand in order to create green waves for many vehicles.
    -   Connection objects from networks parsed via [Sumolib](/Tools/Sumolib "wikilink") can now return *getTLLinkIndex* as well as *getJunctionIndex*.

<!-- -->

-   TraCI
    -   Added function *simulationStep()* to the [C++ TraCI library](/TraCI/C%2B%2BTraCIAPI "wikilink").

### Other

-   Documentation
    -   Online documentation of [TraCI4J](http://github.com/egueli/TraCI4J) can now be found at [traci4j-javadoc](http://sumo.dlr.de/daily/javadoc/traci4j/)
    -   The section on [Additional NETCONVERT outputs was completely rewritten](/Networks/Further_Outputs#Further_Outputs "wikilink").
    -   Added a [new page on XML Validation](/XMLValidation "wikilink")
    -   Added [documentation for the C++ TraCI API client](/TraCI/C%2B%2BTraCIAPI "wikilink")
    -   Added documentation on [route probe detectors](/Simulation/Output/RouteProbe "wikilink") (which was quite overdue).
    -   Expanded documentation on [Calibrators](/Simulation/Calibrator "wikilink") in regard to their mechanism for generating new vehicles.
    -   Added [overview page for simulation routing](/Simulation/Routing "wikilink").

<!-- -->

-   Simulation
    -   Attribute names of the [energy model (battery device, charging stations)](/Models/Electric "wikilink") were updated to bring them in line with naming conventions. Refer to the documentation for new attribute names.

<!-- -->

-   NETCONVERT
    -   Network version is now **0.25**. New features that justify the version change are:
        -   New linkstate *Z* and junction type *zipper* for zipper merging.
        -   New junction type *traffic_light_right_on_red*. To accommodate this type of junction, linkstate 's' (stop) is now allowed in traffic light plans.
        -   Multiple connections to the same lane do not result in a warning any more. (The conflict is resolved using zipper merging or priority right of way)
        -   New network attributes *lefthand*, *junctionCornerDetail* and *junctionLinkDetail*
        -   Note, that the network version should have been updated in 0.23.0 due to the introduction of ships but this was forgotten.

<!-- -->

-   SUMO-GUI
    -   The visualization options *Show internal edge name* and *Show crossing and walkingarea name* were moved from the *Streets*-tab to the *Junctions*-tab.

<!-- -->

-   Tools
    -   *extractRouteEdges.py* was removed as the functionality is now fulfilled by [*route2sel.py*](/Tools/Routes#route2sel.py "wikilink").
    -   [server.py](/Tools/Import/OSM "wikilink") was renamed to [osmWebWizard.py](/Tools/Import/OSM "wikilink") and now resides directly within the *tools* folder.

<!-- -->

-   Misc
    -   *start-commandline-bat* now adds python (python 2.7 in it's default install location) and /tools to the path.
    -   Simplified runner script of [Tutorials/TraCI4Traffic_Lights](/Tutorials/TraCI4Traffic_Lights "wikilink")
