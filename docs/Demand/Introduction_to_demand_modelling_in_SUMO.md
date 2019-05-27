---
layout: post
title: Demand Introduction to demand modelling in SUMO
permalink: /Demand/Introduction_to_demand_modelling_in_SUMO/
---

After having generated a network, one could take a look at it using [SUMO-GUI](/SUMO-GUI "wikilink"), but no cars would be driving around. One still needs some kind of description about the vehicles. This is called the *traffic demand*. From now on we will use the following nomenclature: A **trip** is a vehicle movement from one place to another defined by the starting edge (street), the destination edge, and the departure time. A **route** is an expanded trip, that means, that a route definition contains not only the first and the last edge, but all edges the vehicle will pass. [SUMO](/SUMO "wikilink") and [SUMO-GUI](/SUMO-GUI "wikilink") need routes as input for vehicle movements. There are several ways to generate routes for SUMO. The choice depends on your available input data:

-   Using trip definitions


As described above, each trip consists at least of the starting and the ending edge and the departure time. This is useful for when you want to create *demand* by hand or when writing your own scripts to import custom data. You may either use [DUAROUTER](/DUAROUTER "wikilink") to turn your trips into routes. See [Demand/Shortest_or_Optimal_Path_Routing](/Demand/Shortest_or_Optimal_Path_Routing "wikilink") and [Demand/Dynamic_User_Assignment](/Demand/Dynamic_User_Assignment "wikilink"), or you may load the trips directly into [SUMO](/SUMO "wikilink") [(more details)](/Demand/Automatic_Routing "wikilink").

-   Using flow definitions


This is mostly the same approach as using trip definitions, but one may join vehicles having the same departure and arrival edge using this method

-   Using Randomization


This is a quick way to get some traffic if you do not have access to any measurements but the results are highly unrealistic. See [Tools/Trip\#randomTrips.py](/Tools/Trip#randomTrips.py "wikilink")

-   Using OD-matrices


Origin-Destination-Matrices (or OD-matrices) are often available from traffic authorities. They have to be converted to trips using [OD2TRIPS](/OD2TRIPS "wikilink"). See [Demand/Importing_O/D_Matrices](/Demand/Importing_O/D_Matrices "wikilink"), [Demand/Shortest_or_Optimal_Path_Routing](/Demand/Shortest_or_Optimal_Path_Routing "wikilink") and [Demand/Dynamic_User_Assignment](/Demand/Dynamic_User_Assignment "wikilink").

-   Using flow definitions and turning ratios


One may also leave out the destination edges for flows and use turning ratios at junctions instead. See [JTRROUTER](/JTRROUTER "wikilink").

-   Using detector data (observation points)


Induction loops and similar devices are commonly used by authorities to measure traffic. Using [DFROUTER](/DFROUTER "wikilink") you may uses this data to generate demand. See [Demand/Routes_from_Observation_Points](/Demand/Routes_from_Observation_Points "wikilink").

-   By hand


You can of course generate route XML-files by hand. See [Definition_of_Vehicles,_Vehicle_Types,_and_Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink").

-   Using population statistics


The program [ACTIVITYGEN](/ACTIVITYGEN "wikilink") can be used to turn population statistics into traffic demand. See [Demand/Activity-based Demand Generation](/Demand/Activity-based_Demand_Generation "wikilink").

-   Using data from other sources


see [SUMO_User_Documentation\#Demand_Modelling](/SUMO_User_Documentation#Demand_Modelling "wikilink")

By now, the SUMO-package contains four applications for generating routes. [DUAROUTER](/DUAROUTER "wikilink") is responsible for importing routes or their definitions from other simulation packages and for computing routes using the shortest-path algorithm by Dijkstra. Additionally, in combination with the simulation, the [DUAROUTER](/DUAROUTER "wikilink") can compute the dynamic user assignment formulated by C. Gawron. [JTRROUTER](/JTRROUTER "wikilink") may be used if you want to model traffic statistically, using flows and turning percentages at junctions. [OD2TRIPS](/OD2TRIPS "wikilink") helps you to convert OD-matrices (origin/destination-matrices) into trips. The [DFROUTER](/DFROUTER "wikilink") computes routes from given observation point measures.