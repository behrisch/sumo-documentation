---
title: Z Changes from Version 0.18.0 to Version 0.19.0
permalink: /Z/Changes_from_Version_0.18.0_to_Version_0.19.0/
---

Version 0.19.0 (27.11.2013)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed broken xml in vtk-output
    -   Fixed crash when using calibrators with discontinuous intervals
    -   instantInductionLoops no longer miscount vehicles which change lanes on the detector edge.
    -   instantInductionLoops now write events in the correct order
    -   instantInductionLoops now propperly register vehicles staying on the detector
    -   fixed invalid speeds when running with step-length &lt; 1 (see [<http://sumo-sim.org/trac.wsgi/ticket/1024> ticket 1024](/http://sumo-sim.org/trac.wsgi/ticket/1024_ticket_1024 "wikilink"))
    -   the departSpeed value of a vehicle can now be as high as laneSpeed \* speedFactor
    -   fixed error in a car-following related formula which was causing collisions (see [<http://sumo-sim.org/trac.wsgi/ticket/1026> ticket 1026](/http://sumo-sim.org/trac.wsgi/ticket/1026_ticket_1026 "wikilink"))
    -   queue-output now correctly measures the length from the start of the queue to the rear of the last standing vehicle and no longer includes one additional minGap
    -   when using <span class="inlxml">speedDev</span> and <span class="inlxml">departSpeed</span>, the distribution will be adapted so that a vehicle can use the specified speed.
    -   The attribute <span class="inlxml">emitted</span> of the [summary](/Simulation/Output/Summary "wikilink") output was renamed to <span class="inlxml">inserted</span>
    -   fixed bug which caused vehicles to brake without good reason (see [<http://sumo-sim.org/trac.wsgi/ticket/1052> ticket 1052](/http://sumo-sim.org/trac.wsgi/ticket/1052_ticket_1052 "wikilink"))
    -   flow on a highway will no longer come to standstill just to let vehicles from an on-ramp merge.
    -   vehicles now manage to change to the necessary lanes much more often and thus avoid having to stop and block upstream traffic.
    -   vehicles now use all lanes of a multi-lane roundabout instead of only the outer lane.
    -   fixed tripinfo output for teleporting vehicles ([ticket 990](http://sumo-sim.org/trac.wsgi/ticket/990))
    -   fixed handling of stops before starting position ([ticket 1056](http://sumo-sim.org/trac.wsgi/ticket/1056))
    -   fixed state loading with vehicle type distributions ([ticket 1080](http://sumo-sim.org/trac.wsgi/ticket/1080))
    -   fixed memory leak of route distributions together with route probes ([ticket 1077](http://sumo-sim.org/trac.wsgi/ticket/1077))
    -   fixed reference counts for routes in state save

<!-- -->

-   SUMO-GUI
    -   Right-click now always resolves to the correct object again. The problem was introduced in 0.18.0 and was triggered by drawing railways
    -   The object locator no longer jumps to an arbitrary location if the requested object is not found

<!-- -->

-   TraCI
    -   TraCI now returns the “netto” occupancy (without minGap) as other outputs do (was [ticket\#932](http://sumo-sim.org/trac.wsgi/ticket/932))
    -   Traffic light program changes via TraCI now takes effect immediately instead of one step later. (Thanks to Christoph Sommer for reporting and fixing this problem)
    -   TraCI respects now the begin time option of a simulation ([ticket 1049](http://sumo-sim.org/trac.wsgi/ticket/1049))

<!-- -->

-   DUAROUTER
    -   fixed crash when repairing routes with intermediate dead-end edges
    -   fixed generation of route distributions with 0 probability for trips where the starting and ending edge were connected

<!-- -->

-   NETCONVERT
    -   fixed bug where roundabouts sometimes had incorrect right-of-way rules
    -   option now works when giving a .net.xml file as input
    -   OSM import no longer fails for non-standard input data (i.e. empty *key* attribute or non-numerical value for *tracks* attribute)
    -   option no longer causes edges with a length above to be removed.

<!-- -->

-   DFROUTER
    -   handling end times correctly ([ticket 428](http://sumo-sim.org/trac.wsgi/ticket/428))

### Enhancements

-   Simulation
    -   Increased Simulation performance when handling lots of traffic lights (rewrote code which was updating traffic lights more often than necessary)
    -   added <span class="inlxml">vType</span>-attribute <span class="inlxml">laneChangeModel</span> for customizing the lane changing behavior. Allowed values are *DK2008* (the model used until version 0.18.0), *JE2013* and *LC2013* (the new default model).
    -   Vehicles moving across junctions now consider the exact crossing points at which their paths intersect with other vehicles when deciding on their speed. This leads to smoother traffic flow across junctions.
    -   Vehicles may now change lanes while driving across junctions if the edge they were coming from has priority (only on networks with merged internal lanes, see NETCONVERT changes). This improves simulation performance, particualarly on multi-lane roundabouts.
    -   Teleport warnings now always include a reason. For a vehicle that is teleported because its waitingTime exceeds time-to-teleport the reason can be:
        -   **wrong lane** when the vehicle was stuck on a lane which did not allow it to continue its route,
        -   **yield** when the vehicle was stuck on an unprioritized road and did not find a gap in traffic or
        -   **jam** when the vehicle could not continue because there was no space on the next lane
    -   conflicts between speed deviation and departure speed are handled more gracefully ([ticket 1035](http://sumo-sim.org/trac.wsgi/ticket/1035))

<!-- -->

-   SUMO-GUI
    -   now drawing blinkers to visualize a vehicles desire to change lanes (this is only noticable if a vehicle cannot change lanes immediately).
    -   added vehicle coloring modes *by offset from best lane* and *by acceleration*
    -   when drawing a vehicles route, the lanes which the vehicle intends to use are highlighted where this is known (previously the rightmost lane was always used).
    -   Added hotkeys Ctrl-A, Ctrl-S, Ctrl-D for running, stopping and stepping the simulation
    -   Added a menu for opening the object locator dialogs. Using the menu hotkeys allows searching for simulation objects without using the mouse.
    -   The vehicle parameter dialog now also contains informations related to the vehicle type.

<!-- -->

-   TraCI
    -   lane change requests now have a higher priority by default and will thus succeed much more frequently.
    -   added the possibility to get the number/IDs of vehicles that begin or end to park or stop, see [TraCI/Simulation_Value_Retrieval](/TraCI/Simulation_Value_Retrieval "wikilink") (was [ticket\#353](http://sumo-sim.org/trac.wsgi/ticket/353))
    -   added [new command *lane change mode (0xb6)*](/TraCI/Change_Vehicle_State "wikilink") to control conflict resolution between TraCI-lane-changing request and lane-changing decisions by the laneChangeModel. It also allows to override safety constrainst and to trigger cooperative speed adjustments to better fulfill change requests.
    -   The python API throws now a TraCIException on recoverable errors (such as an unknown vehicle id) and brings the system in a consistent state ([ticket 1043](http://sumo-sim.org/trac.wsgi/ticket/1043))
    -   added possibility to remove waiting cars inspired by Bob Holcomb ([ticket 942](http://sumo-sim.org/trac.wsgi/ticket/942))
    -   improved execution speed of context subscriptions

<!-- -->

-   NETEDIT
    -   added option for reversing the direction of edges
    -   lanes can now be selected based on their index

<!-- -->

-   NETCONVERT
    -   when specifying connections it is now possible to refer to edges which got split ([ticket 492](http://sumo-sim.org/trac.wsgi/ticket/492))
    -   added new projection option to convert Gauss-Krueger to UTM

<!-- -->

-   DUAROUTER
    -   major refactoring of input parsing, it is now possible to mix trips, flows and vehicles in one file
    -   stops are respected on routing ([ticket 988](http://sumo-sim.org/trac.wsgi/ticket/988))

### Other

-   NETCONVERT
    -   reworked type-related warnings when importing OSM data to increase readability
    -   modified naming conventions for internal lanes: previously every internal lane had its own internal edge. The id of this internal edge was “:<junction_id>_<link_index>” and the id of the internal lane was “:<junction_id>_<link_index>_0”. Now Internal lanes with the same start and end edge have a common internal edge (except for lanes following an internal junction). The id of this internal edge is “:<junction_id>_<link_index_of_first_lane>” and the id of the internal lanes is “:<junction_id>_<link_index>_<lane_index>”. The following relation still holds between link indices of internal lanes and their ids: <interal_edge_id> + <internal_lane_id> == <link_index>. The change was done to allow lane changing on internal lanes. As a side effect of merging internal lanes into a single edge, lane lengths may differ compared to the previous release. This is because the simulation length of a lane is always the average of the geometrical length of all lanes of an edge.

<!-- -->

-   TraCI
    -   The documentation for vehicle value [retrieval](/TraCI/Vehicle_Value_Retrieval "wikilink")/[modification](/TraCI/Change_Vehicle_State "wikilink") now includes information on setting/retrieving vehicle-type related values for individual vehicles (i.e. length, maxSpeed).
    -   removed obsolete vehicle add command
    -   TraCI version is now 7

<!-- -->

-   reworked checks for gdal and fox in configure
-   documentation now contains links to the wiki pages it was generated from
