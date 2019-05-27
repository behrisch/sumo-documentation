---
layout: post
title: Simulation Output
permalink: /Simulation/Output/
---

Introduction
============

[SUMO](/SUMO "wikilink") allows to generate a large number of different measures. All write the values they collect into files or a socket connection following the common rules for [writing files](/Basics/Using_the_Command_Line_Applications#Writing_files "wikilink"). Per default, all are disabled, and have to be triggered individually. Some of the available outputs ([raw vehicle positions dump](/Simulation/Output/RawDump "wikilink"), [trip information](/Simulation/Output/TripInfo "wikilink"), [vehicle routes information](/Simulation/Output/VehRoutes "wikilink"), and [simulation state statistics](/Simulation/Output/Summary "wikilink")) are triggered using command line options, the others have to be defined within s.

Available Output Files
======================

Below, the available outputs are listed, joined into groups of topic/aggregation type. Further information about each output can be found by following its link.

vehicle-based information, disaggregated
----------------------------------------

-   [raw vehicle positions dump](/Simulation/Output/RawDump "wikilink"): all vehicle positions over time
    *contains*: positions and speeds for all vehicles for all simulated time steps
    *used for*: obtaining movements of nodes (V2V, for ns-2)
-   [vehicle type probe](/Simulation/Output/VTypeProbe "wikilink"): positions of vehicles over time for a certain vehicle type (or all vehicles)
-   [emission output](/Simulation/Output/EmissionOutput "wikilink"): emission values of all vehicles for every simulation step
-   [full output](/Simulation/Output/FullOutput "wikilink"): various informations for all edges, lanes and vehicles (good for visualisation purposes)
-   [vtk output](/Simulation/Output/VTKOutput "wikilink"): generates Files in the well known [VTK](http://www.vtk.org/) (Visualization Toolkit) format, to show the positions the speed value for every vehicle
-   [fcd output](/Simulation/Output/FCDOutput "wikilink"): Floating Car Data includes name, position, angle and type for every vehicle
-   [trajectories output](/Simulation/Output/AmitranOutput "wikilink"): Trajectory Data following includes name, position, speed and acceleration for every vehicle following the Amitran standard
-   [lanechange output](/Simulation/Output/Lanechange "wikilink"): Lane changing events with the associated motivation for changing for every vehicle
-   [surrogate safety measures](/Simulation/Output/SSM_Device "wikilink"): Output of safety related measures, headway, brake rates, etc

simulated detectors
-------------------

-   [Inductive loop detectors (E1)](/Simulation/Output/Induction_Loops_Detectors_(E1) "wikilink"): simulated induction loops
-   [Instant induction loops](/Simulation/Output/Instantaneous_Induction_Loops_Detectors "wikilink"): simulated unaggregated induction loops
-   [Lane area detectors (E2)](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink"): detectors that capture a lane segment (i.e. simulated vehicle tracking cameras)
-   [Multi-Entry-Exit detectors (E3)](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink"): simulators that track traffic in an area by detecting entry and exit events at defined locations
-   [Route Detectors](/Simulation/Output/RouteProbe "wikilink"): detector for sampling route distributions

values for edges or lanes
-------------------------

-   [edgelane traffic](/Simulation/Output/Lane-_or_Edge-based_Traffic_Measures "wikilink"): edge/lane-based network performance measures
-   [aggregated Amitran measures](/Simulation/Output/Amitran_Traffic_Measures "wikilink"): edge/lane-based network performance measures following the Amitran standard
-   [edgelane emissions](/Simulation/Output/Lane-_or_Edge-based_Emissions_Measures "wikilink"): edge/lane-based vehicular pollutant emission
-   [edgelane noise](/Simulation/Output/Lane-_or_Edge-based_Noise_Measures "wikilink"): edge/lane-based vehicular noise emission; based on Harmonoise
-   [queue output](/Simulation/Output/QueueOutput "wikilink"): lane-based calculation of the actual tailback in front of a junction

values for junctions
--------------------

-   [Tools/Output\#generateTLSE1Detectors.py](/Tools/Output#generateTLSE1Detectors.py "wikilink") script for generating induction loop detectors around all TLS-controlled intersections
-   [Tools/Output\#generateTLSE2Detectors.py](/Tools/Output#generateTLSE2Detectors.py "wikilink") script for generating lane-area detectors around all TLS-controlled intersections
-   [Tools/Output\#generateTLSE3Detectors.py](/Tools/Output#generateTLSE3Detectors.py "wikilink") script for generating multi-entry-exit detectors around all TLS-controlled intersections or for an arbitrary list of intersections. The detectors can be configured to either aggregated or separate the approaching edges and to include or exclude the junction interior.

vehicle-based information
-------------------------

-   [trip information](/Simulation/Output/TripInfo "wikilink"): aggregated information about each vehicle's journey
-   [vehicle routes information](/Simulation/Output/VehRoutes "wikilink"): information about each vehicle's routes over simulation run
-   [stop output](/Simulation/Output/StopOutput "wikilink"): information about vehicle [stops](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink") and loading/unloading of persons and containers
-   [battery usage](/Models/Electric#battery-output "wikilink"): information about battery state for electric vehicles

simulation(network)-based information
-------------------------------------

-   [simulation state statistics](/Simulation/Output/Summary "wikilink"): information about the current state of the simulation

[traffic lights-based information](/Simulation/Output/Traffic_Lights "wikilink")
--------------------------------------------------------------------------------

-   [traffic light states](/Simulation/Output/Traffic_Lights#TLS_States "wikilink"): information about the state (lights) of a traffic light
-   [stream-based traffic light switches](/Simulation/Output/Traffic_Lights#TLS_Switches "wikilink"): information about the switches of a traffic light signal responsible for a certain link
-   [traffic light states, by switch](/Simulation/Output/Traffic_Lights#TLS_Switch_States "wikilink"): information about the states (lights) of a traffic light signal, written only when changed
-   [areal detectors coupled to tls](/Simulation/Output/Traffic_Lights#Coupled_Areal_Detectors "wikilink"): simulated vehicle tracking cameras triggered by tls

Additional Debugging Outputs
----------------------------

-   The option saves debugging data for the intersection model. This data reveals how long each vehicle intends to occupy an upcoming intersection.
-   The option saves debugging data for the interaction between vehicle devices, lanes and output facilities. It is only available when compiling [SUMO](/SUMO "wikilink") with debug flags.

Commandline Output (verbose)
============================

When running the simulation with option (short ) the following data will be printed (unless explicitly disabled with option ):

Vehicle Counts
--------------

-   Inserted: number vehicles that entered the simulation network
-   Loaded: number of vehicles that were loaded from route files. This may differ from emitted forw two reason:
    -   Running with option with a value less than 1.0
    -   Having a congested network where not all vehicles could be inserted before the simulation time ended
-   Running: number of vehicles currently active in the network at simulation end
-   Waiting: number of vehicles which could not yet be inserted into the network due to congestion
-   Teleports: number of of times that vehicles were teleported for any of the following reasons (These reasons are given whenever a teleport warning is issued)
    -   [Collision](/Simulation/Why_Vehicles_are_teleporting#Collisions "wikilink"): a vehicle violated its minGap requirement in relation to its leader vehicle
    -   [Timeout](/Simulation/Why_Vehicles_are_teleporting#Waiting_too_long.2C_aka_Grid-locks "wikilink"): a vehicle was unable to move for --time-to-teleport seconds (default 300)
        -   wrong lane: a vehicle was unable to move because it could not continue its route on the current lane and was unable to change to the correct lane
        -   yield: a vehicle was unable to cross an intersection where it did not have priority
        -   jam: a vehicle could not continue because there was no space on the next lane

If the simulation contained persons the following output will be added:

-   Inserted: number of persons that were loaded from route files
-   Running: number of persons active in the network at simulation end
-   Jammed: number of times a person was jammed

Timing Data
-----------

-   Duration: The amount of elapsed time (as measure by a clock hanging on the wall) while computing the simulation.
-   “Real time factor”: The quotient of *simulated time* / *computation time*. If one hour is simulated in 360 seconds the real time factor is 10.
-   UPS: (updates per second). The number of vehicles that were simulated on average per second of computation time.

If routing took place in the simulation, Each routing algorithm instance will report

-   The number of routing queries
-   The number of edges that were checked in order to find the best route
-   The total time spend routing and the average time per routing call

Aggregated Traffic Measures
---------------------------

When setting the option , verbose output is automatically enabled (unless explicitly set to *false*) and the following averages for all vehicle trips will be printed:

-   RouteLength: average route length
-   Duration: average trip duration
-   WaitingTime: average time spent standing (involuntarily)
-   TimeLoss: average time lost due to driving slower than desired (includes WaitingTime). The desired speed takes the vehicles [speedFactor](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Speed_Distributions "wikilink") into account.
-   DepartDelay: average time vehicle departures were [delayed due to lack of road space](/Simulation/VehicleInsertion "wikilink")

If the simulation contained pedestrians (walking persons) the following output will be added:

-   walks: the number of distinct -elements in the input
-   RouteLength: average walk length
-   Duration: average walk duration

If the simulation contained passengers (persons riding in vehicles) the following output will be added:

-   Rides: the number of distinct -elements in the input
-   Duration: average ride duration
-   Bus rides: number of rides with a public transport vehicle driving on roads (public transport is identified by having the *line*-attribute set).
-   Train rides number of rides with a public transport vehicle driving on rails
-   Bike rides: number of rides with vehicle class *bicycle*
-   Aborted rides: rides that could not be completed because no suitable vehicle was available

When setting this option and using [SUMO-GUI](/SUMO-GUI "wikilink"), the network parameter dialog will also show a running average for these traffic measures (The dialog is accessible by right-clicking on the network background).