---
title: Z Changes from Version 0.19.0 to Version 0.20.0
permalink: /Z/Changes_from_Version_0.19.0_to_Version_0.20.0/
---

Version 0.20.0 (11.03.2014)
---------------------------

### Bugfixes

-   Simulation
    -   Fixed bug in the computation of safe velocities. Sometimes the velocity was too high (causing collisions) but most times it was too low (degrading traffic flow).
    -   Vehicles now move to the right lane after passing instead of staying on the passing lane. (see )
    -   Fixed simulation crash related to lane-changing.
    -   Fixed bug where vehicles would no longer stop on the correct lane if they already stopped on the wrong lane.
    -   Fixed bug which would cause collisions due to unsafe lane changes
    -   Fixed crash when terminating the simulation while vehicles were performing continuous lane changing maneuvers (using option )
    -   Fast vehicles can now be correctly inserted closely in front of slow vehicles .
    -   Rerouting fixed for vehicles which are on internal lanes when the rerouting is requested .
-   SUMO-GUI
    -   Fixed crash when using the object locator on some versions of Ubuntu\].
    -   Fixed bug where brake lights were shown even though the vehicle was not braking
    -   Fixed bug where train carriages where sometimes drawn onto the wrong lane
    -   The vehicle option 'select foes' now works correctly for foe vehicles on internal lanes
    -   Fixed rare graphical glitch when drawing concave junction shapes
    -   Fixed drawing of segmented vehicles (trains) which are longer than their departPos
-   NETCONVERT
    -   Fixed bug which gave some links the wrong priority thus causing collisions (see [ticket \#1096](http://sumo-sim.org/trac.wsgi/ticket/1096#comment:5))
    -   Fixed crash when specifying connections from/to edges which are removed during network building
    -   OSM import no longer fails when encountering empty strings in places where numerical values are expected.
    -   Fixed bug where permissions involving the vClasses **custom1** and **custom2** were not written correctly.
    -   Fixed bug where connections from a lane were sometimes indexed in the wrong order.
    -   Disconnected nodes can no longer be joined into a cluster when using the option .
    -   Fixed [crash](http://sumo-sim.org/trac.wsgi/ticket/1177) when using option
    -   option no longer creates ramps if one of the involved connections is a turnaround
    -   traffic lights which get new programs are no longer renamed (see [ticket 1157](http://sumo-sim.org/trac.wsgi/ticket/1157))
-   DFRouter
    -   Fixed crash/infinite loop when using option . Use of this option is not (yet) recommended (see [ticket 1198](http://sumo-sim.org/trac.wsgi/ticket/1198))
-   JTRRouter
    -   Fixed handling of empty flows (no vehicles) together with a specified start time (see [ticket 1109](http://sumo-sim.org/trac.wsgi/ticket/1109))
-   TraCI
    -   instantInductionLoops are no longer included when calling calling traci.inductionloop.getIDList()
-   Tools
    -   Fixed bug which prevented traceExporter.py from running
    -   Fixed bug which caused all speed values in NS2 output to be 0
    -   Fixed bug which prevented traceExporter.py option from taking effect

### Enhancements

-   Simulation
    -   The summary of teleporting vehicles now lists all teleports according to their reason
    -   Vehicles now perform an emergency braking maneuver to prevent driving across a red light. If this happens in a simulation it usually indicates that the length of the yellow-phase is to short in relation to the road speed and the braking capabilities. To enable driving across red lights, additional TraCI flags were added (see below).
    -   Improved intersection model which results in less conflicts between vehicles with intersecting trajectories while on internal lanes.
    -   Added a first version of the [PHEMlight](/Models/Emissions/PHEMlight "wikilink") emission model (contribution of TU Graz)
    -   Rerouting now keeps existing stops and adds new stops which are part of the new route even in cyclic routes
-   SUMO-GUI
    -   Reworked drawing of trains to have more realistic [carriage lengths](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Visualization "wikilink"). Also some busses are drawn with flexible segments now.
    -   The vehicle parameter dialog now lists the maximum speed of the vehicle's type and the the time headway to the vehicle's current leader
    -   added vehicle coloring mode *by time headway*
    -   Traffic light colors now distinguish between *green major* (code **G**) and *green minor* (code **g**) by coloring the minor state with a darker color.
    -   The lane color scheme *by vClass* now gives fine-grained control over coloring by using the [permission bitmask](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") to select the color.
    -   Added menu option Edit-&gt;Select lanes which allow...-&gt;*vClass*. Together with the street-coloring option *by selection* this allows an easy overview of the road network permitted for a given *vClass*.
    -   Added junction visualization option to disable drawing of junction shapes.
    -   The vehicle coloring mode *by max speed* now factors in the speed limit on the current lane and the speedFactor of the vehicle. The same color thresholds as in coloring *by speed* are now used.
-   NETCONVERT
    -   added option which imports elevation data from OSM input (default *false*).
    -   Conflicts between connections originating from the same edge are now recognized. This can be used to model interaction between right turning vehicles and straight moving non-vehicular traffic on a lane further right.
    -   improved the heuristic for determining junction clusters to be joined when using option . This results in fewer invalid joins. Candidate clusters for manual intervention are indicated.
-   TraCI
    -   added method <span class="inlxml">traci.simulation.convert3D()</span> which converts a road position to either x,y,z or lon,lat,alt
    -   added additonal bits to the traci command [Change Vehicle State/speed mode](/TraCI/Change_Vehicle_State "wikilink") to configure the behavior at intersections. This can be used to make vehicles ignore right-of-way rules and also to force them to drive across a red light.
    -   added optional argument 'flags' to traci.vehicle.setStop() in accordance with the [Vehicle modification API specification](/TraCI/Change_Vehicle_State "wikilink")
    -   the [API to Areal Lane Detectors was added](/TraCI/Lane_Area_Detector_Value_Retrieval "wikilink"); thanks to Mario Krumnow and Robbin Blokpoel
    -   it is now possible to retrieve the leading vehicle within a specified range [Vehicle API specification](/TraCI/Vehicle_Value_Retrieval "wikilink")
    -   a vehicle may be added using a full specification (which is available via XML input)
-   Tools
    -   added tool [xml2csv.py](/Tools/Xml#xml2csv.py "wikilink") which converts all of the XML-output files written by SUMO to a flat-file (CSV) format which can by opened with most spread-sheet software
    -   added tool [csv2xml.py](/Tools/Xml#csv2xml.py "wikilink") for the opposite conversion, requiring an XML schema and also for conversion to Google's protocol buffers [xml2protobuf.py](/Tools/Xml#xml2protobuf.py "wikilink")
    -   osm/osmGet.py now supports retrieving very large areas by bounding box using the option . (previously this option was only supported together with option which has severe size limitations}}
    -   added option to [traceExporter.py](/Tools/TraceExporter "wikilink") which allows exporting vehicle trajactories as [GPX files](http://en.wikipedia.org/wiki/GPS_eXchange_Format)
    -   added option to [traceExporter.py](/Tools/TraceExporter "wikilink") which allows exporting vehicle trajectories as [POIs](/Simulation/Shapes#POI_.28Point_of_interest.29_Definitions "wikilink")
    -   added option to [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") which ensures that generated trips only depart and arrive at edges permitted for *vclass*
    -   [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") now recognizes the network fringe even if the network contains turn-around connections (An edge belongs to the fringe if it contains only incoming or outgoing connections excepting turnarounds). This is important when using the option for generating plausible through-traffic in small networks.
    -   added two [tools for visualising emission behaviour](/Tools/Emissions "wikilink")
    -   added some [visualisation tools](/Tools/Visualization "wikilink")

### Other

-   TraCI
    -   TraCI version is now 8
    -   fixed [documentation of of command **slow down**](/TraCI/Change_Vehicle_State "wikilink"): It changes speed smoothly over the given number of milliseconds (in contrast to command **speed** which changes using maximum acceleration/deceleration).
-   All Applications
    -   Added option with possible values *never*, *always* and *auto* defaulting to *auto*. This causes all input files to be validated against their respective schema, provided the schema-URL is declared in the toplevel XML-Tag (*always* requires the schema-URL to be present).
    -   Added option to all applications which read <span class="inlxml">.net.xml</span>-files which works like option but applies only to sumo networks (default *never* since network validation is computationally expensive).
    -   Most of the input and output files have an XML schema now, see <http://www.sumo-sim.org/trac.wsgi/browser/trunk/sumo/data/xsd>
