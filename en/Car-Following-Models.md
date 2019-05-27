---
layout: post
title: Car-Following-Models
permalink: /Car-Following-Models/
---

Car-Following Models
====================

This overview page collects information regarding car-following models in [SUMO](/SUMO "wikilink"). It is still a stub and needs be expanded.

Links
-----

-   [Publications on car-following models](/Publications#Car-Following_Models "wikilink")
-   [How to implement a new car-following model](/Developer/How_To/Car-Following_Model "wikilink")
-   [More implementation notes on car-following models](/Developer/Implementation_Notes/Vehicle_Models "wikilink")

Model Parameters
----------------

Most car-following models have their own set of parameters. Because some models have a common ancestry they share some parameters. These are described below.

### actionStepLength

This parameter is used to decouple the simulation step length (option ) from the frequency of driver decision making. It can be set either in the -definition as attribute *actionStepLength* or by setting a default value for all vTypes using option .

By default, the action step length is equal to the simulation step length which works well for the default step length of 1s. When performing sub-second simulation by setting a lower step-length value, it may be useful to maintain a higher action step length in order to model reaction times and also in order to reduce computational demand and thus speed up the simulation.

### tau

This parameter is intended to model a drivers desired time headway (in seconds). It is used by all models. Drivers attempt to maintain a minimum time gap of tau between the rear bumper of their leader and their own front-bumper + minGap to assure the possibility to brake in time when their leader starts braking and they need tau seconds reaction time to start breaking as well. The real reaction time is fundamentally limited by the simulation step size ([SUMO](/SUMO "wikilink") option ), resp. the action step length (option , parameter ). For that reason a value of tau below this step-size may lead to collisions if the leader suddenly starts braking hard. If tau is larger then step-size the situation is safe but drivers will still react during each simulation step unless the option is used.