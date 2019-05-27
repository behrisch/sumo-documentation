---
title: Simulation Safety
permalink: /Simulation/Safety/
---

__FORCETOC__

Collisions
==========

[SUMO](/SUMO "wikilink") tracks gaps between vehicles that are on the same edge either fully or partially. By default, whenever these gaps are reduced to below a vehicles *minGap* a collision is registered (default 2.5m). This (potentially) surprising behavior is used to detect issues with the default car-following model that is supposed to never reduce the gap below the minGap. By setting the option this threshold can be reduced. When setting , only *physical collisions* (i.e. front and back bumper meet or overlap) are registered.

When setting the option , collisions between vehicles on the same intersection are also checked by detecting overlap of the vehicles shapes.

The consequence of a collision is configured using the option using one of the following keywords:

-   **teleport**: (the default): the follower vehicle is moved (teleported) to the next edge on its route
-   **warn**: a warning is issued
-   **none**: no action is take
-   **remove**: both vehicles are removed from the simulation

Additionally there is the possibility of stopping vehicles for a fixed time before the *collision action* takes place. This allows for pile-ups and traffic disturbance. To enable stopping, the option must be set with the stopping time in seconds.

Deliberately causing collisions
-------------------------------

To force collisions at a set time, TraCI must be used. Besides setting the speed, it is also necessary to disable safety checks using [the commands speedMode and laneChangeMode](/TraCI/Change_Vehicle_State "wikilink").

To create rear-end collisions with some probability one can configure vehicles with a value of *tau* that is lower than the simulation step size (default 1s) and use the default Krauss model.

Collisions at intersections may be caused by any of the following:

-   yellow phases which are too short in relation to the vehicle speed (giving insufficient time to come to a stop). By default this causes strong braking (*Warning: emergency braking*) potentially followed by rear-end collisions
-   Green phases that allow conflicting streams to drive at the same time. Collision beyond the intersection due to this are always detected but collisions on the intersection are only registered when setting the option .
-   [Double connections](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink") from a traffic-light-controlled edge: If two lanes from the same edge with the same target lane get the green light at the same time, collisions are likely
-   If all [Double connections](/Networks/Building_Networks_from_own_XML-descriptions#Multiple_connections_from_the_same_edge_to_the_same_target_lane "wikilink") at an edge are configured with
-   If connections from the minor road of a priority junction are configured with

To simulate the **effects** of an accident see [FAQ\#How_to_simulate_an_accident](/FAQ#How_to_simulate_an_accident "wikilink").

Reaction Times
==============

In Reality, drivers take actions with some delay in regard to the evolving traffic situation. This reaction time is modelled in the simulation in various ways.

Simulation Step Length
----------------------

All simulation vehicles select their speed simultaneously with regard to the traffic state from the previous simulation step. This means, there is at least a reaction time of the simulation step-length.

In contrast, lane-changing within an edge happens sequentially (in the upstream direction) within each step . Consequently, two vehicles that are driving almost parallel on a 3-lane road may both change their lanes in parallel within a single simulation step because the vehicle further behind already takes into account the lateral movement of the vehicle ahead.

Action Step Length
------------------

By default, vehicles recompute their speed and lane-changing decisions every simulation step. When running with sub-second time resultion (i.e. ), this also gives very low effective reaction times.

To decouple the decision interval from the simulation step length, the vehicle *action-step-length* can be defined as the duration between subsequent vehicle decisions. Decision-making starts direclty after insertion which means vehicles inserted at different times may take decisions during different simulation steps. During simulation steps without decision-making, vehicle positions are updated according to the previously computed acceleration. Lateral dynamics (when using the sublane model) use a dynamic acceleration curve that to complete the current lateral driving manoeuvre.

The action step length can be defined in any of the following ways:

-   setting the option which sets the default action step length for all vehicles
-   setting the attribute *actionStepLength*
-   calling *traci.vehicle.setActionStepLength*

Safety-related parameters
=========================

Simulation of unsafe behavior is a developing subject. Expect model additions and extensions. The following [vehicle type parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") are safety related:

car-following model
-------------------

-   **speedFactor**: higher value causes speeding (driving above the speed limit)
-   **accel**, **decel**: higher values lead to abrupt speed changes
-   **tau**: lower values lead to reduced gaps to the leader vehicle. When setting tau lower than the simulation parameter (default 1s), resp. the vehicle's action step length ( or vehicle parameter `actionStepLength`), collisions may occur
-   **emergencyDecel**: this is the maximum deceleration a vehicle can take to avoid an accident. By default this takes the same value as **decel**
-   **apparentDecel**: this is the deceleration value that will be assumed by other vehicles of the configured vehicle. By default this takes the same value as **decel**

Lane-Changing Model
-------------------

-   lcCooperative: lower values cause less cooperation during lane changing
-   lcSpeedGain: higher values cause more overtaking for speed
-   lcKeepRight: lower values cause less driving on the right
-   lcPushy: setting this to values between 0 and 1 causes aggressive lateral encroachment (only when using the [Sublane Model](/Simulation/SublaneModel "wikilink"))
-   lcAssertive: setting this values above 1 cause acceptance of smaller longitudinal gaps in proportion to driver impatience(only when using the [Sublane Model](/Simulation/SublaneModel "wikilink"))

Junction Model
--------------

There are further parameters which affect safety-related junction behavior. For a description see [Definition_of_Vehicles,_Vehicle_Types,_and_Routes\#Junction_Model_Parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Junction_Model_Parameters "wikilink").

-   impatience: higher values lead to acceptance of smaller time gaps at intersections. These are still safe in the sense of collision avoidance.
-   jmCrossingGap: lower values lead to more aggressive driving at pedestrian intersections (safe)
-   jmDriveAfterRedTime: Violate red lights some time after the switch (safety decreases with growing values)
-   jmDriveRedSpeed: Speed when violating red lights (higher values decrease safety)
-   jmIgnoreFoeProb: Probability to ignore foes with right-of-way (higher values decrease safety)
-   jmIgnoreFoeSpeed: Foe speed threshold which prevents fast vehicles from being ignored (Higher values decrease safety)
-   jmSigmaMinor: When planning to pass a minor link, optimum acceleration is assumed. (higher values cause reduced acceleration and thus decrease time gaps and safety)
-   jmTimegapMinor: Minimum time gap when passing a minor link ahead of a prioritzed vehicle (lower values decrease safety)

Safety-Related Outputs
======================

-   [Surrogate Safety Measures](/Simulation/Output/SSM_Device "wikilink") (headway, brake rates, time to collision etc.)
-   The [Instant Induction Loop](/Simulation/Output/Instantaneous_Induction_Loops_Detectors "wikilink") output records the *gap* attribute which gives the time gap between successive vehicles with sub-second precision.
-   The [Lanechange output](/Simulation/Output/Lanechange "wikilink") generates a record of all lane-changes that take place in the simulation. It includes the longitudinal gap to the leader and follower vehicle on the target lane (both the actual gap and the one that would have been required to ensure stringent deceleration bounds under all circumstances). When using the [sublane model](/Simulation/SublaneModel "wikilink"), the attribute *latGap* records the lateral gap to the neighboring vehicle in the direction of the change if such a vehicle exists.
