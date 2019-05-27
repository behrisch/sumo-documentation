---
title: Other File Extensions
permalink: /Other/File_Extensions/
---

Native SUMO Files
-----------------

To ease the usage of the supplied files, all of which are within a XML-derivate, we use a naming convention for the file extensions to allow a distinction between the contents at first sight. The list of used extensions is shown below. We of course highly encourage you to use this pattern.

-   Configuration files (always the first four letters of the corresponding executable with “cfg” appended)
    -   **\*.sumocfg** (formerly .sumo.cfg): Configuration file for [SUMO](/SUMO "wikilink") and [SUMO-GUI](/SUMO-GUI "wikilink") ([xsd](http://sumo.dlr.de/xsd/sumoConfiguration.xsd))
    -   **\*.netccfg** (formerly .netc.cfg): Configuration file for [NETCONVERT](/NETCONVERT "wikilink") ([xsd](http://sumo.dlr.de/xsd/netconvertConfiguration.xsd))
    -   **\*.netgcfg** (formerly .netg.cfg): Configuration file for [NETGENERATE](/NETGENERATE "wikilink") ([xsd](http://sumo.dlr.de/xsd/netgenerateConfiguration.xsd))
    -   **\*.duarcfg** (formerly .rou.cfg): Configuration file for [DUAROUTER](/DUAROUTER "wikilink") ([xsd](http://sumo.dlr.de/xsd/duarouterConfiguration.xsd))
    -   **\*.jtrrcfg** (formerly .jtr.cfg): Configuration file for [JTRROUTER](/JTRROUTER "wikilink") ([xsd](http://sumo.dlr.de/xsd/jtrrouterConfiguration.xsd))
    -   **\*.dfrocfg** (formerly .df.cfg): Configuration file for [DFROUTER](/DFROUTER "wikilink") ([xsd](http://sumo.dlr.de/xsd/dfrouterConfiguration.xsd))
    -   **\*.od2tcfg** (formerly .od2t.cfg): Configuration file for [OD2TRIPS](/OD2TRIPS "wikilink") ([xsd](http://sumo.dlr.de/xsd/od2tripsConfiguration.xsd))
    -   **\*.acticfg** (formerly .act.cfg): Configuration file for [ACTIVITYGEN](/ACTIVITYGEN "wikilink") ([xsd](http://sumo.dlr.de/xsd/activitygenConfiguration.xsd))

<!-- -->

-   Data files
    -   **\*.net.xml**: network file ([xsd](http://sumo.dlr.de/xsd/net_file.xsd), [description](/Networks/SUMO_Road_Networks "wikilink"))
    -   **\*.rou.xml**: routes file ([xsd](http://sumo.dlr.de/xsd/routes_file.xsd), [description](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink"))
    -   **\*.rou.alt.xml**: route alternatives file ([xsd](http://sumo.dlr.de/xsd/routes_file.xsd), [description](/Demand/Dynamic_User_Assignment#General_behavior "wikilink"))
    -   **\*.add.xml**: [SUMO](/SUMO "wikilink")/[SUMO-GUI](/SUMO-GUI "wikilink") - ([xsd](http://sumo.dlr.de/xsd/additional_file.xsd), [missing description](/missing_description "wikilink"))
        -   traffic lights only ([xsd](http://sumo.dlr.de/xsd/tllogic_file.xsd), [missing description](/missing_description "wikilink"))
    -   **\*.edg.xml**: [NETCONVERT](/NETCONVERT "wikilink") - edges file ([xsd](http://sumo.dlr.de/xsd/edges_file.xsd), [description](/Networks/Building_Networks_from_own_XML-descriptions#Edge_Descriptions "wikilink"))
    -   **\*.nod.xml**: [NETCONVERT](/NETCONVERT "wikilink") - nodes file ([xsd](http://sumo.dlr.de/xsd/nodes_file.xsd), [description](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink"))
    -   **\*.con.xml**: [NETCONVERT](/NETCONVERT "wikilink")- connection file ([xsd](http://sumo.dlr.de/xsd/connections_file.xsd), [description](/Networks/Building_Networks_from_own_XML-descriptions#Connection_Descriptions "wikilink"))
    -   **\*.typ.xml**: [NETCONVERT](/NETCONVERT "wikilink")- edge types file ([xsd](http://sumo.dlr.de/xsd/types_file.xsd), [description](/SUMO_edge_type_file "wikilink"))
    -   **\*.trips.xml**: trip definitions for [DUAROUTER](/DUAROUTER "wikilink"),[SUMO](/SUMO "wikilink") ([description](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Incomplete_Routes_.28trips_and_flows.29 "wikilink"))
    -   **\*.flows.xml**: flow definitions for [JTRROUTER](/JTRROUTER "wikilink"),[DUAROUTER](/DUAROUTER "wikilink"),[SUMO](/SUMO "wikilink") ([description](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Incomplete_Routes_.28trips_and_flows.29 "wikilink"))
    -   **\*.turns.xml**: turn and sink definitions for [JTRROUTER](/JTRROUTER "wikilink") ([xsd](http://sumo.dlr.de/xsd/turns_file.xsd), [description](/Demand/Routing_by_Turn_Probabilities "wikilink"))
    -   **\*.taz.xml**: traffic analysis zones (or districts) file mainly for [OD2TRIPS](/OD2TRIPS "wikilink"),[DUAROUTER](/DUAROUTER "wikilink"),[SUMO](/SUMO "wikilink") ([xsd](http://sumo.dlr.de/xsd/taz_file.xsd)) ([description](/Demand/Importing_O/D_Matrices#Describing_the_TAZ "wikilink"))

<!-- -->

-   Output files
    -   **\*.xml**: inductive loop output ([xsd](http://sumo.dlr.de/xsd/det_e1_file.xsd), \[Simulation/Output/Induction_Loops_Detectors_(E1)|description\]\])
    -   **\*.xml**: areal lane detector output ([xsd](http://sumo.dlr.de/xsd/det_e2_file.xsd), [description](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink"))
    -   **\*.xml**: areal lane detector output ([xsd](http://sumo.dlr.de/xsd/det_e3_file.xsd), [description](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink"))
    -   **\*.xml**: emissions output ([xsd](http://sumo.dlr.de/xsd/emission_file.xsd), [description](/Simulation/Output/EmissionOutput "wikilink"))
    -   **\*.xml**: fcd output ([xsd](http://sumo.dlr.de/xsd/fcd_file.xsd), [description](/Simulation/Output/FCDOutput "wikilink"))
    -   **\*.xml**: full output ([xsd](http://sumo.dlr.de/xsd/full_file.xsd), [description](/Simulation/Output/FullOutput "wikilink"))
    -   **\*.xml**: meandata output ([xsd](http://sumo.dlr.de/xsd/meandata_file.xsd), [description](/Simulation/Output/VTypeProbe "wikilink"))
    -   **\*.xml**: netstate output ([xsd](http://sumo.dlr.de/xsd/netstate_file.xsd), [description](/Simulation/Output/VTypeProbe "wikilink"))
    -   **\*.xml**: queue output ([xsd](http://sumo.dlr.de/xsd/queue_file.xsd), [description](/Simulation/Output/QueueOutput "wikilink"))
    -   **\*.xml**: summary output ([xsd](http://sumo.dlr.de/xsd/summary_file.xsd), [description](/Simulation/Output/Summary "wikilink"))
    -   **\*.xml**: tripinfo output ([xsd](http://sumo.dlr.de/xsd/tripinfo_file.xsd), [description](/Simulation/Output/TripInfo "wikilink"))
    -   **\*.xml**: vtypeprobe output ([xsd](http://sumo.dlr.de/xsd/vtypeprobe_file.xsd), [description](/Simulation/Output/VTypeProbe "wikilink"))

<!-- -->

-   Other files
    -   **\*.xml**: edge diff ([xsd](http://sumo.dlr.de/xsd/edgediff_file.xsd), [missing description](/missing_description "wikilink"))

Imported Files
--------------

-   **\*.osm**: OpenStreetMap XML databases as imported by [NETCONVERT](/NETCONVERT "wikilink") and [POLYCONVERT](/POLYCONVERT "wikilink"), see [OpenStreetMap file](/OpenStreetMap_file "wikilink")
-   **\*.xodr**: OpenDRIVE XML network files as imported by [NETCONVERT](/NETCONVERT "wikilink")
-   **\*.inp**: VISSIM network files as imported by [NETCONVERT](/NETCONVERT "wikilink")
-   **\*.net**: VISUM network files as imported by [NETCONVERT](/NETCONVERT "wikilink") and [POLYCONVERT](/POLYCONVERT "wikilink"), see [Networks/Import/VISUM](/Networks/Import/VISUM "wikilink")
-   **\*.shp, \*.shx, \*.dbf**: ArcView-network descriptions (shapes, shape indices, definitions) as imported by [NETCONVERT](/NETCONVERT "wikilink") and [POLYCONVERT](/POLYCONVERT "wikilink")
-   **\*.xml**:
    -   MATSim road networks as imported by [NETCONVERT](/NETCONVERT "wikilink"), see [Networks/Import/MATsim](/Networks/Import/MATsim "wikilink")

Exported Files
--------------

-   **\*.xml**:
    -   MATSim road networks, see [Networks/Further Outputs](/Networks/Further_Outputs "wikilink")
    -   OMNET: mobility-traces, see [Tools/TraceExporter](/Tools/TraceExporter "wikilink")
    -   Shawn: snapshot-files, see [Tools/TraceExporter](/Tools/TraceExporter "wikilink")
-   **\*.xodr**: OpenDRIVE XML network, see [Networks/Further Outputs](/Networks/Further_Outputs "wikilink")
-   **\*.tcl**: ns2/ns3 trace-files, activity-files, and mobility-files, see [Tools/TraceExporter](/Tools/TraceExporter "wikilink")
-   **\*.dri**, **\*.str**, **\*.fzp**, **\*.flt**: PHEM input files, see [Tools/TraceExporter](/Tools/TraceExporter "wikilink")
-   **unknown**:
    -   GPSDAT, see [Tools/TraceExporter](/Tools/TraceExporter "wikilink")
