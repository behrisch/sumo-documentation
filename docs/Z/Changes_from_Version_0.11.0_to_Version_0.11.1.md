---
title: Z Changes from Version 0.11.0 to Version 0.11.1
permalink: /Z/Changes_from_Version_0.11.0_to_Version_0.11.1/
---

-   All
    -   configuration xml format changed again to <span class="inlxml">
        <section>
        <key value="val"/>

        </section>
        </span> (use /tools/10to11.py to convert from old to new representation)

    -   Bugs in Dijkstra implementation fixed (affecting at least duarouter, routing with traci and automatic rerouting) (01.10.2009)

<!-- -->

-   Simulation
    -   debugged problems when loading TLS definitions with T=0
    -   implemented a [variable car-following model API](/VariableCarModel "wikilink"); many thanks to Tobias Mayer and Christoph Sommer for the collaboration who did most of the work.
    -   debugged occurence of negative vehicle speeds during emit
    -   reworked the mean data output (handling multiple lanes correctly)

<!-- -->

-   GUISIM
    -   implemented [request 1641989: No view reset on reload](http://sourceforge.net/tracker/?func=detail&aid=1641989&group_id=45607&atid=443424).
    -   the number of colors used for range visualization is now variable
    -   debugged problems with not shown junction names

<!-- -->

-   NETCONVERT
    -   making projection mandatory for OSM and DLR-Navteq networks (03.09.2009)
    -   removed option  - was not properly working anyway (02.09.2009)
    -   removed support for “old” TIGER networks - assuming the current ones are given as shape files; is now mapped onto (02.09.2009)
    -   removed support for “split” Elmar networks (option ) (02.09.2009)
    -   renamed to (02.09.2009)
    -   renamed to (02.09.2009)
        -   please note, that all subsequent options have been adapted (but the old names still work as aliases)
    -   added the possibility to define [changes of lane numbers along an edge](/Networks/Building_Networks_from_own_XML-descriptions#Road_Segment_Refining "wikilink") in XML-descriptions (03.09.2009)
    -   replaced by and which determine the correct parameters for the two widely used projections from the input data
    -   for developers: using same loading procedure for all imported networks, see [Developer/How To/Net Importer](/Developer/How_To/Net_Importer "wikilink")

<!-- -->

-   TraCI
    -   debugging sending/receiving messages with length&gt;255 bytes
    -   added further [traffic lights variable retrieval options](/TraCI/Traffic_Lights_Value_Retrieval "wikilink")
    -   added further [induction loops variable retrieval options](/TraCI/Induction_Loop_Value_Retrieval "wikilink")
    -   added further [multi-entry/multi-exit detectors variable retrieval options](/TraCI/Multi-Entry/Multi-Exit_Detectors_Value_Retrieval "wikilink")
    -   added further [junction variable retrieval options](/TraCI/Junction_Value_Retrieval "wikilink")
    -   added further [vehicle variable retrieval options](/TraCI/Vehicle_Value_Retrieval "wikilink")
    -   added further possibilities to [change vehicle values](/TraCI/Change_Vehicle_State "wikilink")
    -   added possibilities to [retrieve edge variables](/TraCI/Edge_Value_Retrieval "wikilink") and [change edge values](/TraCI/Change_Edge_State "wikilink")
    -   added possibilities to [retrieve lane variables](/TraCI/Lane_Value_Retrieval "wikilink") and [change lane values](/TraCI/Change_Lane_State "wikilink")
    -   added possibilities to [change PoI values](/TraCI/Change_PoI_State "wikilink") and to [change polygon values](/TraCI/Change_Polygon_State "wikilink")
    -   added the possibility assign a vehicle a new route via TraCI

<!-- -->

-   DFROUTER
    -   debugged problems with induction loop measure with time&gt;end time
    -   debugged problems with spaces in induction loop measures

<!-- -->

-   OD2TRIPS
    -   debugged problems with O/D matrices that have no comments, was: [defect 148: od2trips breaks on matrices without comments](http://apps.sourceforge.net/trac/sumo/ticket/148); thanks to Wilson Wong for pointing us to it
