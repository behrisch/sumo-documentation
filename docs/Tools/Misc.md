---
title: Tools Misc
permalink: /Tools/Misc/
---

__FORCETOC__

createVehTypeDistributions.py
=============================

Creates a vehicle type distribution by sampling from configurable value distributions for the [desired -parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink").

Example use

` ``/tools/createVehTypeDistributions.py config.txt`

The only required parameter is the configuration file in the format shown below (*example config.txt*):

` tau; normal(0.8,0.1)`
` sigma; normal(0.5,0.2)`
` length; normal(4.9,0.2); [3.5,5.5]`
` vClass; passenger`
` carFollowModel; Krauss`

In the config file, one line is used per vehicle type attribute. The syntax is: nameOfAttribute; valueOfAttribute \[; limits\]

ValueOfAttribute can be a string, a scalar value or a distribution definition. Available distributions and its syntax are: “normal(mu,sd)” with mu and sd being floating numbers: Normal distribution with mean mu and standard deviation sd. “uniform(a,b)” with limits a and b being floating numbers: Uniform distribution between a and b. “gamma(alpha,beta)” with parameters alpha and beta: Gamma distribution.

Limits are optional and defined as the allowed interval: e.g. “\[0,1\]” or “\[3.5,5.0\]”. By default, no negative values are accepted but may be enabled by setting a negative lower limit.

Additional options:

-   configures the name of the output file to be written

-   Name of the created distribution

-   Number of s to be sampled for filling the distribution

-   Set the seed for the random number generator

Retrieving parameters from measurements of individual vehicles
--------------------------------------------------------------

To obtain mean and deviation a number of values must be obtained from the data set. The following is recommenced:

-   **accel**: the maximum (or high percentile) acceleration for each vehicle
-   **deccel**: the maximum (or high percentile) deceleration for each vehicle
-   **speedFactor**: the maximum (or high percentile) quotient of speed/speedLimit for each vehicle

generateTurnDefs.py
===================

This script allows generation of the turn definitions based on the number of lanes allowing particular turns. The basic functionality distributes the traffic uniformly, that is:

1.  distribute the incoming traffic uniformly across the lanes forming the road
2.  distribute the amount of traffic assigned to each lane uniformly among the destinations that the lane allows turns to.
3.  sum up the values for each of the destinations that the road being processed allows turning to.

Example use

` ``/tools/turn-defs/generateTurnDefs.py --connections-file connections.con.xml --turn-definitions-file output.turndefs.xml`

The script allows to be extended with new traffic distribution policies (for example, based on Gaussian distribution) easily. See the *DestinationWeightCalculator* class for details.

The script processes the connections given in the provided *\*.con.xml* file. For usage details, execute the *generateTurnDefs.py* script with *--help* option.

generateParkingLots.py
======================

This skript generats parking lots.

Example use

` ``/tools/generateParkingLots.py -b `<xmin, ymin, xmax, ymax>` -c `<connecting edge>
` [-i `<parking-id>` -n `<number of parking spaces>` -l `<space-length>` -a `<space-angle>` ...]`

or

` ``/tools/generateParkingLots.py -x `<x-pos>` -y `<y-pos>` -c `<connecting edge>
` [-i `<parking-id>` -n `<number of parking spaces>` -l `<space-length>` -a `<space-angle>` ...]`

The required parameter are the shape (--bounding-box) or the position (--x-axis and --y-axis) of the parking lot and the connecting edge (--connecting-edge). More options can be obtained by calling <SUMO_HOME>/tools/generateParkingLots.py --help.

Additional options:

-   defines the name/id of the parking lot

-   defines the number of the parking spaces

-   defines the begin position of the enterance/exit of the parking lot

-   defines the end position of the enterance/exit of the parking lot

-   defines the length of each parking space

-   defines the angle of the parking spaces

-   defines the lateral distance (x-direction) between the locations of two parking spaces

-   defines the longitudinal distance (y-direction) between the locations of two parking spaces

-   defines the rotation degree of the parking lot

-   defines the modification rate of x-axis if the rotation exists

-   defines the modification rate of y-axis if the rotation exists

-   output suffix

-   full name of parking area

-   tell me what you are doing

