---
layout: post
title: Tools Sumolib
permalink: /Tools/Sumolib/
---

**sumolib** is a set of python modules for working with sumo networks, simulation output and other simulation artifacts. For a detailed list of available functions see the [pydoc generated documentation](http://sumo.dlr.de/daily/pydoc/sumolib.html). You can [browse the code here](https://github.com/DLR-TS/sumo/tree/master/tools/sumolib).

__TOC__

importing **sumolib** in a script
=================================

To use the library, the /tools directory must be on the python load path. This is typically done with a stanza like this:

` import os, sys`
` if 'SUMO_HOME' in os.environ:`
`     tools = os.path.join(os.environ['SUMO_HOME'], 'tools')`
`     sys.path.append(tools)`
` else:   `
`     sys.exit(`“`please`` ``declare`` ``environment`` ``variable`` ``'SUMO_HOME'`”`)`

usage examples
==============

import a network and retrieve nodes and edges
---------------------------------------------

` # import the library`
` import sumolib`
` # parse the net`
` net = sumolib.net.readNet('myNet.net.xml')`

` # retrieve the coordinate of a node based on its ID`
` print net.getNode('myNodeID').getCoord()`

` # retrieve the successor node ID of an edge`
` nextNodeID = net.getEdge('myEdgeID').getToNode().getID()`

compute the average and median edge length in a *plain xml* edge file
---------------------------------------------------------------------

` # compute the average length`
` lengthSum = 0.0`
` edgeCount = 0`
` for edge in sumolib.output.parse('myNet.edg.xml', ['edge']):`
`     lengthSum += float(edge.length)`
`     edgeCount += 1`
` avgLength = lengthSum / edgeCount`

` # compute the median length using the `[`Statistics`](http://sumo-sim.org/daily/pydoc/sumolib.miscutils.html#Statistics)` module`
` edgeStats = sumolib.miscutils.Statistics(`“`edge`` ``lengths`”`)`
` for edge in sumolib.output.parse('myNet.edg.xml', ['edge']):`
`     edgeStats.add(float(edge.length))`
` avgLength = edgeStats.median()`

locate nearby edges based on the geo-coordinate
-----------------------------------------------

` # (requires module `[`pyproj`](https://code.google.com/p/pyproj/)` to be installed)`
` # for larger networks `[`rtree`](https://pypi.org/project/Rtree/)` is also strongly recommended`
` radius = 0.1`
` x, y = net.convertLonLatXY(lon, lat)`
` edges = net.getNeighboringEdges(x, y, radius)`
` # pick the closest edge`
` if len(edges) > 0:`
`   distancesAndEdges = sorted([(dist, edge) for edge, dist in edges])`
`   dist, closestEdge = distancesAndEdges[0]`

parse all edges in a route file
-------------------------------

` for route in sumolib.output.parse_fast(`“`myRoutes.rou.xml`”`, 'route', ['edges']):`
`     edge_ids = route.edges.split()`
`     # do something with the vector of edge ids`

coordinate transformations
--------------------------

` x, y = traci.vehicle.getPosition(vehID)`
` lon, lat = traci.simulation.convertGeo(x, y)`
` x2, y2 = traci.simulation.convertGeo(lon, lat, fromGeo=True)`