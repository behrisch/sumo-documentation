---
layout: post
title: Simulation SublaneModel
permalink: /Simulation/SublaneModel/
---

Sublane-Model
=============

This page describes simulations with increased lateral resolution. This model is useful to simulate the following:

-   multiple 2-wheeled vehicles driving in parallel on a single lane
-   vehicles overtaking a bicycle on a single lane
-   formation of virtual lanes in dense traffic (i.e. 3 vehicles driving in parallel on 2 lanes)
-   virtual lane formation for emergency traffic
-   lateral dynamics
    -   lateral acceleration and speed
    -   blocking of 2 lanes during overtaking
    -   bicycles drive on the rightmost side of a lane
    -   lateral encroachment by aggressive drivers
    -   dynamic longitudinal gap acceptance during lane changing

This model is activated using the option . The model is described in *Simulation framework for testing ADAS in Chinese traffic situations* [in proceedings of SUMO2016](http://elib.dlr.de/106342/1/SUMOconference_proceedings_2016.pdf)

New Parameters
--------------

The vehicle behavior is subject to model-specific [vType attributes (maxSpeedLat, minGapLat, latAlignment)](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") and [lane-changing-modell attributes (lcSublane, lcPushy)](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Lane-Changing_Models "wikilink").

When describing the state of a vehicle in [SUMO-GUI](/SUMO-GUI "wikilink")-dialogs or in the [netstate-output](/Simulation/Output/RawDump "wikilink"), additional attributes are used:

-   lateral position (posLat): offset from the center of the current lane in meters
-   shadow lane: Each vehicle in the sublane model occupies 1 or 2 lanes. The lane that contains that contains the center of the front-bumper is refered to as its *lane*. If the vehicle front-bumper also reaches into another lane, this is called the *shadow lane*
-   target lane: if the vehicle has started a lane changing manoeuvre to another lane, this is the target lane
-   lateral speed: the lateral velocity in the current simulation step
-   lane change maneuver distance: the absolute lateral distance to be covered in the current lane change maneuver in m (overtaking another vehicle is considered to consist of two maneuveres: 1. leaving the current lane, 2. re-entering the lane after overtaking)
-   right side on edge: offset of the right vehicle side from the right side of the current road edge in m
-   left side on edge: offset of the left vehicle side from the right side of the current road edge in m
-   right edge sublane: the rightmost sublane that the vehicle occupies (at least partially) when counting all sublanes of the current edge beginning at 0 on the right side of the edge
-   left edge sublane: the leftmost sublane that the vehicle occupies (at least partially) when counting all sublanes of the current edge beginning at 0 on the right side of the edge

Model Details
-------------

The regular lanes of the road network are divided into sublanes with a minimum width of the given resolution (). If the lane width is not a multiple of the given value, the leftmost sublane has a reduced with. The default lane-width of SUMO is 3.2m so a lateral resolution of 0.8 will created exactly 4 sublanes of that width per lane. A resulution of 1.0 will create three sublanes of 1.0m width and on more lane of 0.2m width. It is recommended use a resolution that is at least as small as the least wide vehicle being simulated (i.e. motorcycles).

### Car-Following

Vehicles occupy one or more sublanes and perform car-following calculations for all vehicles that are being followed on at least one sublane.

### Lane-Changing

The lane-changing model *SL2015* is automatically used when enabling the sublane model. Lane-changing takes place at the sublane level and potentially uses the whole width of the road according to the width of the vehicles. Besides changing for route-following, cooperation, obligation (keepRight) or speed gain, vehicles also perform lateral movement to achieve a certain lateral alignment. This preference for either staying in the middle of a lane or to one of its sides is configured with the vType attribute .

In addition to these motivation, an additional behavioral layer is responsible for maintaining safe lateral gaps. The desired gap can be set using the vType attribute . Distances keeping is only performed in regard to vehicles that are not too far behind the ego vehicle. If the front bumper of a neighbouring vehicle is behind the longitudinal midpoint of the ego vehicle, that neighbour is ignored.

The model *SL2015* supports these additional parameters:

-   **lcSublane**: The eagerness for using the configured lateral alignment within the lane. Higher values result in increased willingness to sacrifice speed for alignment. default: 1.0, range \[0-inf\]
-   **lcPushy**: Willingness to encroach laterally on other drivers. default: 0, range \[0-1\] If this is set, vehicles will start to change laterally even though their target sublanes(s) are still occupied. For urgent (strategic) lane-changes this produces behavior where the ego vehicle violates the lateral minimum gap of its neighbor and thereby triggers evasive lateral movement (pushing).
-   **lcAssertive**: Willingness to accept lower front and rear gaps on the target lane. default: 0, range 0 to 1
-   **lcImpatience**: dynamic factor for modifying lcAssertive and lcPushy. default: 0 (no effect) range -1 to 1. Impatience acts as a multiplier. At -1 the multiplier is 0.5 and at 1 the multiplier is 1.5
-   **lcTimeToImpatience**: Time to reach maximum impatience (of 1). Impatience grows whenever a lane-change manoeuvre is blocked.
-   **lcAccelLat**: maximum lateral acceleration per second. Together with *maxSpeedLat* this constrains lateral movement speed.

### Misc

Vehicles can be located laterally anywhere on the lane(s). Vehicles change lanes incrementally depending on their *maxSpeedLat* vType-attribute. The width of sublanes affects the fidelity of car following in regard to the acceptance of lateral gaps and also determines the number of candidate movements that are evaluated during lane-changing.

When [controlling vehicles via-TraCI using the vehicle command moveToXY](/TraCI/Change_Vehicle_State#move_to_XY_.280xb4.29 "wikilink"), vehicles will be placed at the exact longitudinal and lateral position to match the specified coordinates. This allows for full control of sublane-placement.

Simple Continous lane-change model
==================================

The sublane model described above allows simulating a wide range of phenomena related to lateral vehicle dynamics at the price of increased computational load.

One important aspect of lateral dynamics is the fact that a lane-change manoeuvre generally takes longer than a single simulation step where is lane-changing is instantaneous without activating the sublane model.

If only the non-instantaneous aspect of lane-changing needs to be modelled, a simplified (and thus faster) model may be used as an alternaive to the sublane model.

The *Simple continous lane-change model* is activated by setting the option which specifies the default time for changing between adjacent lanes in seconds (instead of setting option .

When using this model, vehicles will move with constant lateral speed to complete a manoeuvre in the specified time. Lane-changing decisions take the extra time required into account.

Additional Vehicle Parameters
-----------------------------

-   when setting the -attribute *maxSpeedLat*, the lateral speed computed from the default duration is replaced by the configured type-specific speed.