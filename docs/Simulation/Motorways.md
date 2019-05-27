---
title: Simulation Motorways
permalink: /Simulation/Motorways/
---

Motorway Simulation
===================

This page describes simulations of motorways in SUMO. It aims to collect best practices when modelling motorway networks and traffic.

Building a network for motorway simulation
==========================================

Networks can be imported from any supported data source or created from scratch with [NETEDIT](/NETEDIT "wikilink"). Depending on the level of detail special processing may be necessary

Motorway ramps
--------------

If the network does not contain detailed ramp data, [NETCONVERT](/NETCONVERT "wikilink") can be [configured to add them heuristically](/Networks/Further_Options#Guessing_On-_and_Off-Ramps "wikilink"). This basically adds acceleration at on-ramps and deceleration lanes at off-ramps.

### Reduction in the number of lanes

The usual way to set up a lane-number reduction is to configure the rightmost lane as a dead-end (no connection to the next edge) and force vehicles to change-lanes to the left. In some situations it may be appropriate to declare the node where the lane number changes as a [zipper node](/Networks/Building_Networks_from_own_XML-descriptions#Node_types "wikilink") instead.

### Combined On-Off-Ramps

Combined ramps are those where the acceleration lane from an on-ramp becomes the deceleration lane for a nearby off-ramp. This forces vehicles into a weaving pattern where entering and exiting vehicles need to swap lanes. This type of situation may cause deadlocks in [SUMO](/SUMO "wikilink") unless preventive measures are taking. The problem is exacerbated if the acceleration/deceleration lane is short or traffic is very dense.

To prevent deadlocks the connection pattern shown in the following image should be used. Note, that the off-ramp is targeted by the two rightmost lanes of the preceding edge and lane 0 has priority over lane 1. Vehicles exiting the motorway will attempt to move to the rightmost lane if possible but can still continue their route if that lane is occupied.

Image:onOffRamp.png|Connectivity at on-off-ramp

Vehicle class specific speed limits
-----------------------------------

In some jurisdictions, certain vehicle classes have specific speed limits (i.e. Trucks which may not drive faster than 90km/h on German motorways). This should be modelled as described here: [Networks/Building_Networks_from_own_XML-descriptions\#vehicle-class_specific_speed_limits](/Networks/Building_Networks_from_own_XML-descriptions#vehicle-class_specific_speed_limits "wikilink")

Lane-changing prohibitions
--------------------------

Symmetrical lane-changing prohibitions between two lanes can be modelled by adding a thin lane with attribute between them.

Defining Motorway Traffic
=========================

Speed Distributions
-------------------

To achieve a realistic scenario, the desired vehicle speeds should be heterogeneous. This can be achieved by setting the [vType-attributes speedFactor and speedDev](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Speed_Distributions "wikilink"). Since a vehicle *speedFactor* defines desired speed relative to the speed limit of each edge, [\#Vehicle_class_specific_speed_limits](/#Vehicle_class_specific_speed_limits "wikilink") should be taken into account.

High Flows
----------

Some tips on how to achieve high flows are described [in the FAQ](/FAQ#How_do_I_get_high_flows.2Fvehicle_densities.3F "wikilink")