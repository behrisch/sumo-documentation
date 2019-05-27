---
title: Tutorials HighwayDetector
permalink: /Tutorials/HighwayDetector/
---

This tutorial describes how to set up a traffic scenario using mainly [NETEDIT](/NETEDIT "wikilink"), [DFROUTER](/DFROUTER "wikilink") and some python tools when you already have a fairly good network source for your simulation site and also a good coverage of the network with detectors giving you aggregated counts (and maybe speeds) of the vehicles in the real world. It is not limited to highways but the preconditions are met there more frequently. The focus is more on demand preparation and calibration and not so much on network tweaking. [thumb|Selected edges (blue) are of minor priority and will be discarded](/File:netedit_select_highway.png "wikilink")

Network
-------

Assuming you are already familiar with network extraction from your favourite mapping source you can open your net with [NETEDIT](/NETEDIT "wikilink") and reduce it to your area of interest. Assume you have a navteq file you can select (and then delete) all edges with a priority of less than -1 to reduce it to a highway network. Afterwards one can use rectangle selection (hold shift) to further limit the area considered. You also might want to enable ramp guessing in the options dialog. If the network has been prepared by an older version of SUMO it is probably a good idea to recalculate all the connections afterwards. Do so by selecting all junctions in select mode and then resetting them in connect mode. There may still be missing ramps and unusual connections which could not be guessed automatically and which should be fixed manually after setting up the basic scenario.

Detector data
-------------

### Locating detectors

Your final network should have locations for induction loops on many of the available edges. If you have detector positions as geo-coordinates it usually requires some manual work to locate the detectors in the network. A starting point can be to use the python sumolib to match the positions to the network:

    sys.path.append(os.path.join(os.environ["SUMO_HOME"], 'tools'))
    import sumolib

    net = sumolib.net.readNet(<NETFILE>)
    detectors = []
    for id, lon, lat in <DETECTORS>:
        xy_pos = net.convertLonLat2XY(lon, lat)
        # look 10m around the position
        lanes = net.getNeighboringLanes(xy_pos[0], xy_pos[1], 10)
        # attention, result is unsorted
        for lane, dist in lanes:
            # now process them and determine a "bestLane"
            # ...
            pos, d = bestLane.getClosestLanePosAndDist(xy_pos)
            detectors.append(sumolib.sensors.inductive_loop.InductiveLoop(id, bestLane.getID(), pos))
    sumolib.files.additional.write(<DETECTORFILE>, ils)

Be aware to have the python rtree library installed if you are working with large networks. It will speed up the geometry lookups tremendously. Depending on the quality of your network and detector location data, you should probably not always choose the closest lane but also consider whether the number of lanes / the speed limit match your expectations. After the initial positioning you can load the file for fine tuning as an additional file into [NETEDIT](/NETEDIT "wikilink").

### Processing input data

A common format for detector data is an aggregation into slots of one minute. The [DFROUTER](/DFROUTER "wikilink") can process files of the following format:

Determining the routes
----------------------

### [DFROUTER](/DFROUTER "wikilink")

### flowrouter.py

### Validation and initial parameters

flowFromRoutes.py

-   maximum flow
-   multiple intervals

Calibrating the data
--------------------

### Speed calibration