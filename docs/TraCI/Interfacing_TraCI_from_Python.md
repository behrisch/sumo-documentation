---
title: TraCI Interfacing TraCI from Python
permalink: /TraCI/Interfacing_TraCI_from_Python/
---

The [TraCI](/TraCI#TraCI_Commands "wikilink") commands are split into the 13 domains gui, lane, poi, simulation, trafficlight, vehicletype, edge, inductionloop, junction, multientryexit, polygon, route, person and vehicle, which correspond to individual modules. For a detailed list of available functions see the [pydoc generated documentation](http://sumo-sim.org/daily/pydoc/traci.html). The source code can be found at [1](http://sumo.dlr.de/trac.wsgi/browser/trunk/sumo/tools/traci)

importing **traci** in a script
-------------------------------

To use the library, the /tools directory must be on the python load path. This is typically done with a stanza like this:

` import os, sys`
` if 'SUMO_HOME' in os.environ:`
`     tools = os.path.join(os.environ['SUMO_HOME'], 'tools')`
`     sys.path.append(tools)`
` else:   `
`     sys.exit(`“`please`` ``declare`` ``environment`` ``variable`` ``'SUMO_HOME'`”`)`

This assumes that the [environment variable **SUMO_HOME**](/Basics/Basic_Computer_Skills#Additional_Environment_Variables "wikilink") is set before running the script. Alternatively, you can declare the path to *sumo/tools* directly as in the line

` sys.path.append(os.path.join('c:', os.sep, 'whatever', 'path', 'to', 'sumo', 'tools'))`

First Steps
-----------

In general it is very easy to interface with SUMO from Python (the following example is a modification of [tutorial/traci_tls](/Tutorials/TraCI4Traffic_Lights "wikilink")):

First you compose the command line to start either [SUMO](/SUMO "wikilink") or [SUMO-GUI](/SUMO-GUI "wikilink") (leaving out the option which was needed before 0.28.0):

`sumoBinary = `“`/path/to/sumo-gui`”
`sumoCmd = [sumoBinary, `“`-c`”`, `“`yourConfiguration.sumocfg`”`]`

Then you start the simulation and connect to it with your script:

`import traci`
`traci.start(sumoCmd) `
`step = 0`
`while step < 1000:`
`   traci.simulationStep()`
`   if traci.inductionloop.getLastStepVehicleNumber(`“`0`”`) > 0:`
`       traci.trafficlight.setRedYellowGreenState(`“`0`”`, `“`GrGr`”`)`
`   step += 1`
`traci.close()`

After connecting to the simulation, you can emit various commands and execute simulation steps until you want to finish by closing the connection. by default the close command will wait until the sumo process really finishes. You can disable this by calling

`traci.close(False)`

Subscriptions
-------------

Subscriptions can be thought of as a batch mode for retrieving variables. Instead of asking for the same variables over and over again, you can retrieve the values of interest automatically after each time step. TraCI subscriptions are handled on a per module basis. That is you can ask the module for the result of all current subscriptions after each time step. In order to subscribe for variables you need to know their variable ids which can be looked up in the traci/constants.py file.

`import traci`
`import traci.constants as tc`
`traci.start([`“`sumo`”`, `“`-c`”`, `“`my.sumocfg`”`]) `
`traci.vehicle.subscribe(vehID, (tc.VAR_ROAD_ID, tc.VAR_LANEPOSITION))`
`print(traci.vehicle.getSubscriptionResults(vehID))`
`for step in range(3):`
`   print(`“`step`”`, step)`
`   traci.simulationStep()`
`   print(traci.vehicle.getSubscriptionResults(vehID))`
`traci.close()`

The values retrieved are always the ones from the last time step, it is not possible to retrieve older values.

Context Subscriptions
---------------------

Context subscriptions work like subscriptions in that they retrieve a list of variables automatically for every simulation stop. However, the do so by setting a reference object and a range and then retrieving variables for all objects of a given type within range of the reference object.

TraCI context subscriptions are handled on a per module basis. That is you can ask the module for the result of all current subscriptions after each time step. In order to subscribe for variables you need to the domain id of the objects that shall be retrieved and the variable ids which can be looked up in the traci/constants.py file. The domain id always has the form CMD_GET_<DOMAIN>_VARIABLE. The following code retrieves all vehicle speeds and waiting times within range (42m) of a junction (the vehicle ids are retrieved implicitly).

`import traci`
`import traci.constants as tc`
`traci.start([`“`sumo`”`, `“`-c`”`, `“`my.sumocfg`”`]) `
`traci.junction.subscribeContext(junctionID, tc.CMD_GET_VEHICLE_VARIABLE, 42, [tc.VAR_SPEED, tc.VAR_WAITING_TIME])`
`print(traci.junction.getContextSubscriptionResults(junctionID))`
`for step in range(3):`
`   print(`“`step`”`, step)`
`   traci.simulationStep()`
`   print(traci.junction.getContextSubscriptionResults(junctionID))`
`traci.close()`

The values retrieved are always the ones from the last time step, it is not possible to retrieve older values.

Adding a StepListener
---------------------

Often a function needs to be called each time when traci.simulationStep() is called, to let this happen automatically (always *after* each call to simulationStep()) it is possible to add a StepListener object 'listener' (more precisely an instance of a subclass of traci.StepListener) i.e.

` class ExampleListener(traci.StepListener):`
`    def step(self, t=0):`
`        # do something at every simulaton step`
`        print(`“`ExampleListener`` ``called`` ``at`` ``time`` ``%s`` ``ms.`”` % t)`
`       `
` listener = ExampleListener()`
` traci.addStepListener(listener)`

Controlling parallel simulations from the same TraCI script
-----------------------------------------------------------

The TraCI python library can be used to control multiple simulations at the same time with a single script. The function *traci.start()* has an optional label argument which allows you to call it multiple times with different simulation instances and labels. The function *traci.switch()* can then be used to switch to any of the initialized labels:

` traci.start([`“`sumo`”`, `“`-c`”`, `“`sim1.sumocfg`”`], label=`“`sim1`”`)`
` traci.start([`“`sumo`”`, `“`-c`”`, `“`sim2.sumocfg`”`], label=`“`sim2`”`)`
` traci.switch(`“`sim1`”`)`
` traci.simulationStep() # run 1 step for sim1`
` traci.switch(`“`sim2`”`)`
` traci.simulationStep() # run 1 step for sim2`

If you prefer a more object oriented approach you can also use connection objects to communicate with the simulation. They have the same interface as the static *traci.* calls but you will still need to start the simulation manually for them:

` traci.start([`“`sumo`”`, `“`-c`”`, `“`sim1.sumocfg`”`], label=`“`sim1`”`)`
` traci.start([`“`sumo`”`, `“`-c`”`, `“`sim2.sumocfg`”`], label=`“`sim2`”`)`
` conn1 = traci.getConnection(`“`sim1`”`)`
` conn2 = traci.getConnection(`“`sim2`”`)`
` conn1.simulationStep() # run 1 step for sim1`
` conn2.simulationStep() # run 1 step for sim2`

Embedded Python
---------------

As an experimental feature, it is also possible to link SUMO with python directly and have the scripts executed in SUMO. The syntax is completely the same, except that you leave out the calls to init and close and you need to start sumo with the option --python-script. This feature is considered deprecated and will be replaced by [libsumo](/libsumo "wikilink"). It does currently *not* work with the GUI version of sumo.

Since the feature is not well tested yet, you need to enable embedded python explicitly when building SUMO (it is *not* enabled in the release versions and the nightly build). In order to do so, follow the instructions below

### Linux

-   install the python devel package files
-   call configure using the --with-python option
-   make && make install as usual

### Windows

-   make sure python is installed and is in your PATH
-   call tools\\build\\pythonPropsMSVC.py to generate / modify the build\\msvc10\\config.props file
-   build the Win32 Release version as usual
-   the debug build is somewhat more involved and is disabled by default, the following instructions are [taken from here](http://upp-mirror.googlecode.com/svn-history/r3552/trunk/bazaar/Py/install.txt)
    -   download the python source package fitting your python version
    -   open the pcbuild.sln in the PCbuild subdir with Visual Studio
    -   do the Win32 Debug build for python, it will have lots of errors but the main parts (hopefully) succeed
    -   from the PCbuild dir copy
        -   python27_d.dll to the Python dir (something like C:\\Python27)
        -   python27_d.lib, python27_d.pdb, python27_d.exp to the libs dir (C:\\Python27\\libs)
        -   every \*_d.pyd to the DLLs dir (C:\\Python27\\DLLs)
    -   enable the python debug build by editing build\\msvc10\\Win32.props
    -   now you can do the Win32 Debug build for SUMO

Earlier versions of Visual Studio and 64bit build are currently not directly supported (but the interested programmer should be able to modify the files accordingly).

Additional Functions
--------------------

When using TraCI there are some common tasks which are not covered by the traci library such as

-   Analyzing the road network
-   Parsing simulation outputs

For this functionality it is recommended to use [Tools/Sumolib](/Tools/Sumolib "wikilink")

Pitfalls and Solutions
----------------------

-   Note that strings, if exchanged, have to be ASCII-encoded.
-   If you start sumo from within your python script using subprocess.Popen, be sure to call wait() on the resulting process object before quitting your script. You might loose output otherwise.

Usage Examples
--------------

### Run a simulation until all vehicles have arrived

`  while traci.simulation.getMinExpectedNumber() > 0: `
`      traci.simulationStep()`

### Add trips (incomplete routes) dynamically

Define a vehicle type that carries a rerouting device in an and load this at the start of the simulation

`   `<vType id="reroutingType">
`       `<param key="has.rerouting.device" value="true"/>
`   `</vType>

Then via TraCI add your vehicle like so:

`   traci.route.add(`“`trip`”`, [`“`startEdge`”`, `“`endEdge`”`])`
`   traci.vehicle.add(`“`newVeh`”`, `“`trip`”`, typeID=`“`reroutingType`”`)`

This will cause the vehicle to compute a new route from startEdge to endEdge according to the estimated travel times in the network at the time of departure. For details of this mechanism see [Demand/Automatic_Routing](/Demand/Automatic_Routing "wikilink").