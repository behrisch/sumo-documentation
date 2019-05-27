---
layout: post
title: TraCI Object Context Subscription
permalink: /TraCI/Object_Context_Subscription/
---

__FORCETOC__

Introduction
============

Context subscriptions are allowing the obtaining of specific values from surrounding objects of a certain so called “EGO” object. With these datas one can determine the traffic status around that EGO object. Such an EGO Object can be any possible Vehicle, inductive loop, points-of-interest, and such like. A vehicle driving through a city, for example, is surrounded by a lot of different and changing vehicles, lanes, junctions, or points-of-interest along his ride. Context subscriptions can provide selected variables of those objects that surround the EGO object within a certain range.

The subscription for a structure's context is initiated using a “Subscribe ... Context” command (0x80-0x8e). The command is evaluated immediately on request, verifying it this way. It returns a “Subscribe ... Context” response (0x90-0x9e). If EGO is a vehicle, the subscription is descheduled as soon as the vehicle leaves the simulation.

As soon as the subscription was accepted, it is executed after each call of [Simulation Step(2)](/TraCI/Control-related_commands#Command_0x02:_Simulation_Step.282.29 "wikilink") command.

The command ID describes the type of the EGO-object which is the center of the context; currently, the following EGO-objects are supported:

| Type               | Command ID | Notes |
|--------------------|------------|-------|
| inductive loops    | 0x80       |       |
| lanes              | 0x83       |       |
| vehicles           | 0x84       |       |
| points-of-interest | 0x87       |       |
| polygons           | 0x88       |       |
| junctions          | 0x89       |       |
| edges              | 0x8a       |       |
||

For a given EGO-structure, each subscription allows to address multiple variables from structures of a certain kind. This means, if you have an EGO-vehicle, you may ask for speeds and positions of vehicles in range of EGO. If you also need information about surrounding points-of-interest, you have to add a further context subscription for PoIs. Vehicles, and PoIs belong to different “context domains”. The following domains are available:

| Type               | Context Domain ID | Notes                                                                     |
|--------------------|-------------------|---------------------------------------------------------------------------|
| inductive loops    | 0xa0              | [retrievable variables](/TraCI/Induction_Loop_Value_Retrieval "wikilink") |
| lanes              | 0xa3              | [retrievable variables](/TraCI/Lane_Value_Retrieval "wikilink")           |
| vehicles           | 0xa4              | [retrievable variables](/TraCI/Vehicle_Value_Retrieval "wikilink")        |
| points-of-interest | 0xa7              | [retrievable variables](/TraCI/POI_Value_Retrieval "wikilink")            |
| polygons           | 0xa8              | [retrievable variables](/TraCI/Polygon_Value_Retrieval "wikilink")        |
| junctions          | 0xa9              | [retrievable variables](/TraCI/Junction_Value_Retrieval "wikilink")       |
| edges              | 0xaa              | [retrievable variables](/TraCI/Edge_Value_Retrieval "wikilink")           |
||

For each domain, the same variables can be retrieved as using the Get ... Variable commands (see above).

Command 0x8<i>X</i>: Subscribe ... Context
==========================================

|            |          |           |                |               |                 |                                 |
|:----------:|:--------:|:---------:|:--------------:|:-------------:|:---------------:|:-------------------------------:|
|    time    |   time   |   string  |      ubyte     |     double    |      ubyte      |            ubyte\[n\]           |
| begin Time | end Time | Object ID | Context Domain | Context Range | Variable Number | The list of variables to return |

Some notes:

-   begin Time: the subscription is executed only in time steps &gt;= this value; in ms
-   end Time: the subscription is executed in time steps &lt;= this value; the subscription is removed if the simulation has reached a higher time step; in ms
-   Context Domain: the type of objects in the addressed object's surrounding to ask values from
-   Context Range: the radius of the surrounding
-   The size of the variables list must be equal to the field “Variable Number”.

Response 0x9<i>X</i>: ... Subscription Response
===============================================

|           |                |                |               |               |                              |                                  |                                              |                        |     |                              |                                  |                                              |                        |     |               |                              |                                  |                                              |                        |     |                              |                                  |                                              |                        |
|:---------:|:--------------:|:--------------:|:-------------:|:-------------:|:----------------------------:|:--------------------------------:|:--------------------------------------------:|:----------------------:|:---:|:----------------------------:|:--------------------------------:|:--------------------------------------------:|:----------------------:|:---:|:-------------:|:----------------------------:|:--------------------------------:|:--------------------------------------------:|:----------------------:|:---:|:----------------------------:|:--------------------------------:|:--------------------------------------------:|:----------------------:|
|   string  |      ubyte     |      ubyte     |      int      |     string    |             ubyte            |               ubyte              |                     ubyte                    |      <return_type>     | ... |             ubyte            |               ubyte              |                     ubyte                    |      <return_type>     | ... |     string    |             ubyte            |               ubyte              |                     ubyte                    |      <return_type>     | ... |             ubyte            |               ubyte              |                     ubyte                    |      <return_type>     |
| Object ID | Context Domain | Variable Count | Objects Count | Object \#1 ID | Object \#1 / Variable \#1 Id | Object \#1 / Variable \#1 status | Object \#1 / Return type of the variable \#1 | Object \#1 / <VALUE#1> | ... | Object \#1 / Variable \#n Id | Object \#1 / Variable \#n status | Object \#1 / Return type of the variable \#n | Object \#1 / <VALUE#n> | ... | Object \#m ID | Object \#m / Variable \#1 Id | Object \#m / Variable \#1 status | Object \#m / Return type of the variable \#1 | Object \#m / <VALUE#1> | ... | Object \#m / Variable \#n Id | Object \#m / Variable \#n status | Object \#m / Return type of the variable \#n | Object \#m / <VALUE#n> |

The respond to a **“Subscribe ... Variable”**.

The status is 0x00 (RTYPE_OK) if the variable could be retrieved successfully. If not, the status is 0xff (RTYPE_ERR). In the second case, the variable type is set to string and the variable value contains the error message. Please note, that the status should be ok in all cases.

-   ***Variable Count*** is the number of returned variables per object
-   ***Objects Count*** is the number of objects in range

This implies that n\*m values are returned (Variable Count \* Objects Count).

Client library methods
======================

-   In the [python library](/TraCI/Interfacing_TraCI_from_Python#Context_Subscriptions "wikilink"), all domains support the methods [*subscribeContext* and *unsubscribeContext*](http://www.sumo.dlr.de/daily/pydoc/traci.domain.html#Domain)
-   In the [C++ library](/TraCI/C%2B%2BTraCIAPI "wikilink"), the method *simulation.subscribeContext* takes an additional argument that encodes the source domain

Notes
=====

-   When asking for domains “point-of-interest” and “polygon”, the current version does not support asking for these structures when their position was changed using TraCI
