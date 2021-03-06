---
layout: post
title: Networks Further Options
permalink: /Networks/Further_Options/
---

[NETCONVERT](/NETCONVERT "wikilink"), [NETGENERATE](/NETGENERATE "wikilink"), and [NETEDIT](/NETEDIT "wikilink") offer some more options to describe how the network shall be imported. The scope of some options does not cover all import types.

Setting default Values
----------------------

It was mentioned, that edge parameter may be omitted and defaults will be used in this case. It is possible to set default values for the imported edges' number of lanes, allowed speed, and priority, using the options (or for short), (or for short), (or for short), respectively.

Adding Turnarounds
------------------

Normally, turnarounds are added as a possible edge continuations and play an important role during network building (see [Publications\#Krajzewicz_et_al2005_2](/Publications#Krajzewicz_et_al2005_2 "wikilink")). Still, one may want not to add them. In this cases, it is possible to disallow their appending using option .

Removing Geometry Nodes
-----------------------

In most input networks one may find nodes where one street comes in and one with the same attributes goes out or where two parallel edges come in and two (with the same attributes) come out. Such nodes have mostly no meaning (maybe besides the additional possibility to make a U-turn) and may be removed. The removal of such nodes increases the simulation speed due to a smaller number of edges to process during each time step. To remove such nodes and join the incoming and outgoing edges use . The removal of nodes preserves the geometry of edges by ading a further geometry point at the removed node's position.

Using Edges' maximum Speed Definitions in km/h
----------------------------------------------

Some people do not like to use speed definitions in m/s. If you want to define the speeds allowed on your edges in km/h instead, you should pass the option to [NETCONVERT](/NETCONVERT "wikilink").

Importing Networks without Traffic Light Logic
----------------------------------------------

Some of the supported network formats supply information about the logic of the traffic lights, other do not. Due to this, we have to compute the traffic lights on our own. Doing this, we not only have to compute the signal plans but also compute which junctions will have traffic lights. There are several options steering this procedure. At first, you have to tell [NETCONVERT](/NETCONVERT "wikilink")/[NETGENERATE](/NETGENERATE "wikilink") that you wish the program to guess positions of traffic lights. This is done using the -option.

You may also set junctions as tls-controlled using or as uncontrolled using . Both options assume to get a list of node names divided by ',' as parameter. The behaviour when a node is in both lists is undefined.

During the computation of tls-logics among other information we have to guess the duration of the phases. The options and allow you to give the durations of green and yellow lights. Both options assume the duration in seconds as an int. The duration of having red is dependent on the number of other phases and their green and yellow phase durations. The green phase length has a default of 31s, yellow lights are - if no value is set for this option - computed using the which is described below.

There is yet no possibility to compute or estimate a “green wave” (synchronized traffic lights to allow continuous flow in one direction). You have only the options to shift the computed phases by half of their duration or by a quarter of their duration. The options for this are: and . Both options assume to get a list of node names divided by ',' as parameter. The behaviour when a node is in both lists or if the node is not meant to be controlled by a tls is undefined. Of course you can also edit the offsets within the generated network file (see [Simulation/Traffic Lights](/Simulation/Traffic_Lights "wikilink")).

Guessing On- and Off-Ramps
--------------------------

Most of the imported network descriptions do not have information about highway on- and off-ramps. This means ramps are connected to the highway without acceleration/deceleration lanes. You can force [NETCONVERT](/NETCONVERT "wikilink") to guess where on- and off-ramps shall be build. To enable this, use the option . The algorithm ensures that acceleration lanes are added on highway junctions with one incoming and one outgoing highway edge and one incoming minor edge and that deceleration lanes are added on highway junctions with one incoming and one outgoing highway edge and one outgoing minor edge. Lanes are only added if the sum of incoming lanes differs from the sum of outgoing lanes. You can constrain the classification of highways by setting a minimum speed of this edge using and the classification of the minor edge is by setting its maximum speed using (both options assume a speed in m/s). Furthermore, tells [NETCONVERT](/NETCONVERT "wikilink") how long the added ramp shall be in meters.

Inner-junction Traffic
----------------------

If you already know SUMO or if you have taken a look at some of the examples you may have noticed that vehicles used to “jump” over a junction instead of driving over them. This behaviour was quite appropriate for simulating large scenarios as in these cases the simulation error could be neglected (at least we have neglected it). Since version 0.10.0 SUMO will by default simulate traffic over the junctions in a way you know it from reality. Because inserting inner lanes into a network dramatically increases the network's size, you may want to return to the old behavior using the option .

Pruning the imported network
----------------------------

[NETCONVERT](/NETCONVERT "wikilink") offers you some possibilities to constrain the read edges what is quite needful if one has a large street network but only wants to simulate a part of it or only the major roads. The first possibility to constrain the input is to name all the edges you want to keep. You can either do this on the command line/within your configuration directly using where each represents the id of an edge you want to keep separated by a ',' or you can save this list into a file where each id is stored in a seperate line and then let [NETCONVERT](/NETCONVERT "wikilink") read this file using . In the case you are joining edges using (see “Removing Geometry Nodes”), you may also be interested in the option which forces [NETCONVERT](/NETCONVERT "wikilink") to join the edges first and remove the unwished afterwards.

It is also possible to constrain the imported edges by giving a minimum velocity that is allowed on an edge in order to include this edge into the generated network. Use for this where is the minimum velocity an edge must allow in order to be included in the output in m/s.