---
layout: post
title: Simulation VehicleSpeed
permalink: /Simulation/VehicleSpeed/
---

There are a wide range of influences on vehicle speed. They are described in the following. Each of these influences sets an upper bound on the vehicle speed. The actual speed in any given situation is the minimum speed of all influences.

maxSpeed
========

The [-attribute ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") models the maximum speed that a vehicle will travel. It can be thought of as the maximum speed of the engine or the maximum speed desired by the driver under any circumstances (possibly these two aspects will be modelled with separate attributes in the future).

edge/lane speed
===============

The -attribute is usually [defined for edges](/Networks/Building_Networks_from_own_XML-descriptions#Edge_Descriptions "wikilink") but may also [differ among the lanes](/Networks/Building_Networks_from_own_XML-descriptions#Lane-specific_Definitions "wikilink") of the same edge. It models the legal speed limit.

When approaching an edge with a lower speed limit than the current one, a vehicle will slow down so as to stay within the new limit at the time of reaching the new edge.

Each vehicle can be [assigned an individual speed multiplier](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Speed_Distributions "wikilink") which then lets it exceed this limit.

Since version 0.24.0 it is also possible to define [vClass-specific speed limits for every edge](/Networks/Building_Networks_from_own_XML-descriptions#vehicle-class_specific_speed_limits "wikilink").

Car Following Model
===================

The [car following model](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Car-Following_Models "wikilink") of a vehicle defines its speed in relation the vehicle ahead. The default model always selects the maximum speed which is *safe* in the sense of being able to stop in time to avoid a collision.

Acceleration and Deceleration
-----------------------------

All models are subject to constraints in their [acceleration an deceleration](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Car-Following_Models "wikilink"). By default they will not accelerate stronger then the *accel* value. The default model plans it's maneuvers so as to stay within the *decel* value (per second) but other models may interpret this value differently. All models will never brake harder than the *emergencyDecel* value (which defaults to the same value as *decel* but may be set independently).

Dawdling
--------

Most car-following models support the -attribute which models driver imperfection. For values above **0**, drivers with the default car-following model will drive *slower* than would be safe by a random amount (between \[0, \]).

Intersections
=============

Vehicles approaching an intersection without the right-of-way have to slow down. If the intersection is used by other vehicles which have the right of way, stopping may be necessary until a safe time-window is found. That time windows is based on the same safety assumptions as the car-following model. For the default *Krauss*-model this means that each vehicle must be able to stop safely even if it's lead vehicle brakes hard to a full stop.

Even if a vehicle has the right-of-way it may need to slow down due to [impatient](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Impatience "wikilink") drivers which drive across the intersection. The [right-of-way rules](/Networks/Building_Networks_from_own_XML-descriptions#Right-of-way "wikilink") at an intersection are [defined by the node -attribute](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink") and by [traffic lights](/Simulation/Traffic_Lights "wikilink").

The visibility of intersections can be controlled by the visibility attribute for the corresponding connections, see [Connection Descriptions](/Networks/Building_Networks_from_own_XML-descriptions#Connection_Descriptions "wikilink"). Per default, a vehicle approaching from a minor road slows down until it is 4.5m away from the intersection (even if no prioritized vehicle is nearby). After that it may start to accelerate again if there is a safe gap in traffic.

Lane Changing
=============

Vehicles may decide to slow down in order to execute a lane-change maneuver. They may also slow down in order to aid other vehicles with lane-changing. If the lane a vehicle is on does not have a connection to the next edge on a vehicles route, the vehicle will decelerate and stop.

Stops
=====

Vehicles will decelerate when approaching the position of a [-definition](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink").

Acceleration / Deceleration constraints
=======================================

Vehicles can only change their speed by a certain amount each time step. This is defined by the [-attributes and ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink")

departSpeed / arrivalSpeed
==========================

Vehicles enter the network using their [defined ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicles_and_Routes "wikilink"). When approaching the end of their route they will adapt their speed to match their [defined ](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicles_and_Routes "wikilink")

Variable Speed Signs
====================

[Variable speed signs](/Simulation/Variable_Speed_Signs "wikilink") are used to modify the speed limit of an edge for a defined time interval.

Calibrators
===========

[Calibrators](/Simulation/Calibrator "wikilink") are used to adapt the flow on an edge for a defined time interval but may also be used to modify the speed limit of an edge.

TraCI
=====

Vehicles can forced to adapt their speed using [TraCI commands](/TraCI/Change_Vehicle_State "wikilink"). When using the command *slow down* stochastic influences on speed are not applied. By using [the *speed mode* command, various safety related influences can be selectively disabled](/TraCI/Change_Vehicle_State#speed_mode_.280xb3.29 "wikilink").