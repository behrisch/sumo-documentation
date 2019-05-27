---
title: FAQ
permalink: /FAQ/
---

General
-------

### What is SUMO?


SUMO is a traffic simulation package. It is meant to be used to simulate networks of a city's size, but you can of course use it for smaller networks and larger, too, if your computer power is large enough.

### What does “SUMO” mean?


“SUMO” is an acronym for “Simulation of Urban MObility”.

### What kind of a traffic simulation is SUMO?


SUMO is mainly a **microscopic**, space-continuous road traffic simulation. It supports multi-modal and inter-modal ground based traffic. SUMO models individual vehicles and their interactions using models for car-following, lane-changing and intersection behavior. It also uses [pedestrian models](/Simulation/Pedestrians "wikilink") to simulate the movement of persons and their interactions with vehicles.

<!-- -->


To allow for the efficient simulation of very large scenarios, it is also possible to run SUMO as a [**mesoscopic** simulation](/Simulation/Meso "wikilink").

SUMO also supports **macroscopic** traffic assignment using the [MAROUTER](/MAROUTER "wikilink") application.

### What is the best way to read the documentation and find out about specific topics


The main page for getting an overview over the various topics is the outline [SUMO_User_Documentation](/SUMO_User_Documentation "wikilink"). If you do not find the topic of interest listed there it is often useful to use google for searching the wiki (it tends to be a lot smarter than the wiki-internal search). Add **sumo** and **wiki** to your search terms and it will generally find the relevant pages.

### How can I contribute to SUMO?

-   Tell us about your extensions on the [developer mailing list](https://accounts.eclipse.org/mailing-list/sumo-dev)
-   Send us patches (bug fixes as well as extensions) either to the same list or as pull requests at <https://github.com/eclipse/sumo> (also see next question).
-   Report bugs (crashes, surprising behavior) or invalid documentation at [sumo-user](https://accounts.eclipse.org/mailing-list/sumo-user) or at <https://github.com/eclipse/sumo/issues>
-   The main development team at the [DLR](http://sumo.dlr.de) is always looking for project partners. [Contact us](/Contact "wikilink") to discuss your proposals.
-   Make your SUMO simulation scenarios publicly available
-   [Cite us](/Publications "wikilink") in your publications and tell other people about SUMO.
-   Answer questions on the [sumo-user mailing list](/Contact "wikilink") whenever you know the answer
-   Contribute to this wiki ([contact us](/Contact "wikilink"), so we can give you editing rights)
-   Create a video tutorial and tell us about it
-   Join us at the annual

### How do code contributions work?


We need to make sure that you have the necessary rights on the code and that you agree that your contribution is put under the Eclipse Public License v2. The easiest way to do achieve this is

-   Create an [Eclipse account](https://accounts.eclipse.org/user/register) if you do not already have one
-   Fill out a simple oline form, called the Eclipse Contributor Agreement (ECA, this is mandatory)
-   Ensure that the email address in git matches your address at Eclipse (look for user.email in the output of git config -l)
-   Make sure all the commits you want to contribute have a valid Signed-off-by entry. If you use command line git, this is as simple as doing “git commit -s” when committing.
    -   if you want to modify an existing commit because you forgot to sign it, you can use “git commit -s --amend”
-   Send us a pull request on GitHub
    -   You can of course send your code by any other means as well but we will need to make sure that you have a valid ECA and the Signed-off-by
-   More info may be found at <https://wiki.eclipse.org/Development_Resources/Contributing_via_Git>

### How do I contribute to the wiki?

-   Alternatively: Send an email stating your preferred user name to sumo@dlr.de
-   wait for our mail telling you that you have edit-permissions

### How do I cite SUMO


Cite using [Krajzewicz_et_al2012](/Publications#Krajzewicz_et_al2012 "wikilink").

### How do I unsubscribe from the mailing list?

Go to <https://lists.sourceforge.net/lists/listinfo/sumo-user>. At the bottom of the page you will find a form that allows you to enter your email address to unsubscribe it from the list.

General Problem Solving
-----------------------

### An application crashed. What should I do?

The applications in the SUMO suite may crash when running out of memory. Monitor the memory usage of your applicatons to check whether that may be your problem. 32bit-applications may only use 2GB of RAM. Use the 64bit version and ensure sufficient memory on your machine in order to work with larger files. If this does not fix the crash, please report this as a bug [as explained below](/FAQ#How_do_I_report_Erroneous_behavior_of_a_SUMO-Application.3F "wikilink").

### Why does SUMO not behave as documented in this wiki?

This wiki documents the behavior of the [latest development version](/Downloads#Nightly_Snapshots "wikilink"). This is usually quite close the the [latest release](/Downloads "wikilink") (differences are explicitly listed in the [ChangeLog](/ChangeLog "wikilink"). If you are using an older version of SUMO, you need to refert to [the documentation that is packaged with that version](/Downloads#SUMO_-_older_releases "wikilink"). Note that we do not back-port bugfixes to older version of SUMO. If possible you should always use the latest version of SUMO.

### There is an error message but I don't know what I did wrong


Activate [XML-Validation](/XMLValidation "wikilink") on your input files. If that does not solve your problem feel free to ask on the mailing list but **please** remember to copy / screenshot the error message itself and attach it to your question. Attaching (zipped!) input files for reproducing the error message is also a good idea (see question above).

### How do I report erroneous behavior of a SUMO application?


If you suspect a bug in one of the applications you should report your findings by sending the following items to the [mailing list](/Contact "wikilink"):

-   a description of the SUMO-version and the operating system you are using
-   a screenshot or error output showing the unexpected behavior (this may allow us to diagnose the problem at a single glance)
-   the complete input files for reproducing the error (i.e. a .sumocfg and all files referenced therein) in a zip-archive. Please remove unnecessary inputs (i.e. only 2 vehicles instead of 2000) and try to find the minimum input example which still shows the problem.
-   a description at which time step (for simulations) and on which edge/junction the problem occurs

### SUMO does not do what I want and I don't know how to solve the issue


See above but **please** give enough details when asking on the mailing list.

### What should I do to get helpful answers on the mailing list?

-   Make your question specific (avoid vague terms).
-   Phrase your question using familiar terms (not everyone is an expert in your domain).
-   Don't ask for too many things in a single post.
-   Do some research on your own before you post the question (otherwise you may appear to be lazy).
    -   read the FAQ
    -   read the documentation
    -   check out the [Tutorials](/Tutorials "wikilink")
    -   do a web search (past questions and answers from the mailing list can be found by google)
-   Do not ask the same thing twice in a short span of time. If you are in a hurry and cannot get an answer, try to change your question according to the above suggestions.
-   Be polite

### My [TraCI](/TraCI "wikilink")-program is not working as intended. Can you help me debug it?


Unfortunately, we do not have the resources to debug other peoples code. If you suspect a bug in TraCI itself, the [general rules of bug-reporting](/FAQ#How_do_I_report_Erroneous_behavior_of_a_SUMO-Application.3F "wikilink") apply. Feel free to post your code to the mailing list as there may be other programmers present who could help. Be aware that someone who wants to reproduce your problem needs all your input files to do so.

### I want to do a project with SUMO can you help me with the implementation?


Unfortunately, we do not have the resources to do other peoples projects for free. [Contact](http://www.dlr.de/ts/en/desktopdefault.aspx/tabid-1231/mailcontact-30303/) us for paid consultancy.

We try to help out with bugs and give pointers to the relevant documentation but this free support is limited to what we can do in our spare time.

Features
--------

### Does SUMO support traffic within the junctions?


Yes, SUMO supports inner-junction traffic since version 0.9.5.

### Is it possible to connect SUMO to an external application (f.e. ns-2)?


There are several approaches to do this, see [TraCI](/TraCI "wikilink") and [Topics/V2X](/Topics/V2X "wikilink")

### Can SUMO simulate lefthand traffic?


Yes. It is supported since version 0.24.0. To build a network for lefthand traffic, the option must be set. Note, that this option exists in earlier versions but only works correctly since 0.24.0.

### Can SUMO generate movement traces?


Yes. This is accomplished by using the [traceExporter](/Tools/TraceExporter "wikilink") tool to convert SUMO outputs into the appropriate format. Also see [Topics/V2X](/Topics/V2X "wikilink")

### Can SUMO simulate heterogeneous traffic / lane-free traffic ?


Yes (since version 0.27.0). The [Sublane-Model](/Simulation/SublaneModel "wikilink") is activated by setting the option .

### Can SUMO simulate driving in reverse?


No. While it is possible to move a vehicle backwards using [TraCI](/TraCI "wikilink"), other vehicles will not react in a sensible manner to this.

### Can SUMO simulate driving through the oncoming lane?


Yes. (since version 0.27.0). The [opposite-direction-driving feature is activated by using a network with additional information](/Simulation/OppositeDirectionDriving "wikilink").

### Can SUMO be run in parallel (on multiple cores or computers)?


The simulation itself always runs on a single core. However, routing in [SUMO](/SUMO "wikilink") or [DUAROUTER](/DUAROUTER "wikilink") can be parallelized by setting the option and respectively.

<!-- -->


The python TraCI library allows controlling multiple simulations from a single script either by calling *traci.connect* and storing the returned connection object or by calling *traci.start(label=...)* and retrieving the connection object with *traci.getConnection(label)*.

Building / Installation
-----------------------

### How do I access the code repository?


Since 2018-04-10 SUMO moved to [the organizational Eclipse account at GitHub](https://github.com/eclipse/sumo/). You have the choice to access the repository using git or subversion. There are plenty of clients for all platforms. If you use the command line client, you can checkout sumo using the following command (for git):

` git clone --recursive `[`https://github.com/eclipse/sumo`](https://github.com/eclipse/sumo)

If you want to see the full project history in your git checkout please change to the created directory and call

` git fetch origin refs/replace/*:refs/replace/*`

For later updates go inside the sumo directory, which has been created, and simply type `git pull`.

### Is there further documentation on Git and Subversion?


There are the [Git book](https://git-scm.com/book/de/v1) and the [Subversion book](http://svnbook.red-bean.com/) and the [GitHub help](https://help.github.com/) is also worth reading.

### How to get an older version of SUMO?


see [Downloads\#SUMO_-_older_releases](/Downloads#SUMO_-_older_releases "wikilink"). On Linux, older versions [must be built from source](/Installing/Linux_Build "wikilink").

### How to check out revision 5499 (or any other outdated sumo)?


You can use the subversion option “**-r <REVISION_NUMBER>**” together with the checkout on the command line. If you are using git you can find the correct hash using the git log. You have to consult your client's documentation if you use a graphical interface. Please be aware of the fact that we can only give very limited support for older versions.

### Which platforms are supported?


We compile regularly under Windows 7 and Windows Server 2012 R2 using Visual Studio 2013 (32bit and 64bit) and have daily builds on Linux (openSUSE Leap 42.1 (64bit) and openSUSE 13.1 (32bit)). Furthermore there are nightly builds on the [open build service](https://build.opensuse.org/package/show?package=sumo_nightly&project=home%3Abehrisch). SUMO can be installed on MacOS via MacPorts (or built from source). We would be happy to hear about successful builds on other platforms. We already heard about successful builds on Solaris and Cygwin.

### Can I run multiple versions of SUMO alongside each other?


Different versions of SUMO generally do not interfere with each other. When setting environment variables such as *SUMO_HOME* or *PATH*, care must be take to reference the desired directory. On linux, the package manager will generally only offer a single version. [All other versions must be built from source](/Installing/Linux_Build "wikilink").

### Letters and words are represented as squares in SUMO-GUI and Netedit


Make sure that your computer supports 3D Acceleration and graphical drivers are correctly installed and configured.

### Troubleshooting


See [Installing/Linux Build](/Installing/Linux_Build "wikilink") or [Installing/Windows Build](/Installing/Windows_Build "wikilink").

### Uninstalling


In most cases you can simply delete the sumo folder. If you installed sumo via a package manager on linux, uninstall it via the package manager as well.

Basic Usage
-----------

### What measures are used/represented?


All time values are given in seconds. All length values are given in meters. This means that speed should be given in m/s, etc.

Currently, the default simulation time step is one second long (to be exact: in each simulation step one second real time is simulated).

### What does the following error mean?


Warning: No types defined, using defaults... Error: An exception occurred! Type:RuntimeException, <Message:The> primary document entity could not be opened. Id=<PATH> Error: (At line/column 1/0). Error: Quitting (conversion failed).

Answer: Simply that the file you try to use (<PATH>) does not exist. This is xerces' way to say “file not found”.

### How do I work around a file not found / command not found error?


To run the command-line programs your operating system must be able to find them.

If you are using Windows please consult [Basics/Basic Computer Skills\#running_programs_from_the_command_line](/Basics/Basic_Computer_Skills#running_programs_from_the_command_line "wikilink")

If you are using Linux run `export PATH=$PATH:/path/to/sumo/bin` (replace /path/to/sumo/bin with the path to the bin directory of your sumo installation)

### How do I work around missing dll errors on windows?


Install [MSVC2013 Redistributable](http://www.microsoft.com/download/en/details.aspx?id=5555) (Old versions of SUMO may also require the MSVC2010 Redistributable)

### What is the meaning of the different exit codes (linux command line)


0 is success, 1 is a recognized error and anything above is an unorderly termination (crash). If you see exit codes other than 0 or 1 [please tell us about it](/FAQ#How_do_I_report_Erroneous_behavior_of_a_SUMO-Application.3F "wikilink")

### What's the deal with *schema resolution* warnings / xsd errors?


Since version 0.20.0 sumo performs [XML-validation](/XMLValidation "wikilink") on input files with schema information. This helps to detect common mistakes during manual preparation of XML input files. Files generated by sumo applications such as [DUAROUTER](/DUAROUTER "wikilink") always add schema information. The schema files which are needed for checking are retrieved from the local sumo installation if [the environment variable **SUMO_HOME** is set](/Basics/Basic_Computer_Skills#Additional_Environment_Variables "wikilink"). Otherwise the files will be retrieved from [sumo.dlr.de](http://www.sumo.dlr.de) which is slower. Validation can be disabled by using the option or by deleting the schema information at the top of the XML input file(s).

### What causes ''Error: unable to resolve host/address 'sumo.dlr.de' ''?


This is related to [XML-validation](/XMLValidation "wikilink") (see above). When the [the environment variable **SUMO_HOME**](/Basics/Basic_Computer_Skills#Additional_Environment_Variables "wikilink") is not set, applications will try to retrieve the xsd schema files online. If there is no internet connection. The above error results. The solution is to either

-   disable validation or
-   declare **SUMO_HOME** or
-   ensure internet connectivity

### Why can my input-XML files not be read even though they look OK to me?


Errors such as

`Error: attribute name expected at `
`At line/column 10/46`


can be caused by non-printing characters in the XML-file. Open your XML-file in a document editor and activate the option for showing line-breaks and other non-printing characters to find them.

### Why do I get errors about *missing files* / *file not found* even though the file exists?


Sumo uses the space character to separate file paths. This means it will not be able to load files with a path such as *C:\\Program Files\\foo.xml* (even when adding quotation marks). Additionally, SUMO may fail to load files if the name contains characters outside the basic [ASCII set](http://en.wikipedia.org/wiki/Ascii).

NETCONVERT
----------

### I made changes to the *.net.xml*-file but it did not work as expected. Why?


As a general rule, you should never modify the *.net.xml* file directly. There are lots of subtle interdependencies between network elements which are hard to get right with manual modifications. Even if your .net.xml can be loaded by [SUMO](/SUMO "wikilink") it could fail in ways that are less obvious:

-   By having right-of-way rules that work somewhat differently than expected (this part of the *.net.xml* file is particularly complex)
-   By losing properties when later being edited with [NETEDIT](/NETEDIT "wikilink")
-   By failing to work with updated versions of [SUMO](/SUMO "wikilink")

If you need to modify a network there are several possibilities:

1.  Edit the network with [NETEDIT](/NETEDIT "wikilink")
2.  Modify the original input files and then rebuild the net with [NETCONVERT](/NETCONVERT "wikilink").
3.  Patch the network with [NETCONVERT](/NETCONVERT "wikilink"). You can [load a *.net.xml* file](/Networks/Import/SUMO_Road_Networks "wikilink") together with [small XML-files](/networks/Building_Networks_from_own_XML-descriptions "wikilink") to patch individual edges, nodes and connections. Additional possibilities are described [here](/Tutorials/ScenarioGuide#Modifying_the_Network "wikilink"). For changing traffic light plans or timings see [Simulation/Traffic_Lights](/Simulation/Traffic_Lights "wikilink"). If you cannot figure out how to accomplish the desired changes this way, [contact us!](/Contact "wikilink").
4.  Use [NETCONVERT](/NETCONVERT "wikilink")-option to convert the network into [it's plain XML representation](/networks/Building_Networks_from_own_XML-descriptions "wikilink"). Then modify these files and rebuild the network

If you need to build a network from custom input data it is recommended to generate [*plain-xml*-files](/Networks/Building_Networks_from_own_XML-descriptions "wikilink") (nodes, edges, connections) with a custom process and build your network with [NETCONVERT](/NETCONVERT "wikilink") from these files. These input files allow for many customization of geometrical and structural network properties. If you cannot get them to represent the network you need, ask for help on the mailing list.

### My network looks ugly, All the junction shapes are wrong. How come?


This currently happens up to version 0.23.0 if you import networks with left-handed traffic. See [\#Can_SUMO_simulate_lefthand_traffic.3F](/#Can_SUMO_simulate_lefthand_traffic.3F "wikilink").

### Some junctions in my network look ugly. What can I do?


See [Joining Junctions](/Networks/Import/OpenStreetMap#Junctions "wikilink"). If that doesn't help, check for invalid edge geometry. A sharp turn in front of an intersection (even if the segment is only centimeters long) may mess up the shape computation. Read the [NETCONVERT](/NETCONVERT "wikilink") warnings about sharp angles and consider using [NETCONVERT](/NETCONVERT "wikilink") option .

If that still doesn't help you may specify the shape of the junction [manually using the -attribute](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink").

### Can I import the free network of Osnabrück “Frida”?


Yes and no. You can import it using NETCONVERT, a description is available at [Networks/Import/ArcView](/Networks/Import/ArcView#.27Frida.27_network_.28city_of_Osnabr.C3.BCck.29 "wikilink").

This may be a good gis-network but lacks some needed information in order to be usable for simulations (see discussion at the link above).

### Are there any other free networks available I can use?


See [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink")

### The application hangs after a while (few memory consumption, most of the system time) (Windows)


You are probably running a program compiled in the debug-mode. This yields in at least the triple of normal memory usage and your system may not be able to solve. Try to use the normal version, build in Release-mode (or buy more RAM :-) ).

### Many errors of the form *Edge's 'x' from- and to-node are at the same position*


You are probably trying to import a network with geo-coordinates without specifying a geo-projection. Add option .

### Many errors of the form *Error: Type 'x' used by edge 'y' was not defined*


You are probably trying to re-import an OSM-network written to plain XML data. Add or provide a type file.

NETEDIT
-------

### How can I obtain NETEDIT?


[NETEDIT](/NETEDIT "wikilink") is available as part of the regular distribution since version 0.25.0.

Traffic Demand Generation
-------------------------

### How do I generate random routes?


First of all you should know that random routes are probably quite unrealistic.

If you wish to use them anyway, use the script /tools/trip/randomTrips.py to generate random trips as explained here [Tools/Trip\#randomTrips.py](/Tools/Trip#randomTrips.py "wikilink").

You can also call the script without options to get additional help.

See [Demand/Shortest or Optimal Path Routing\#Usage_Examples](/Demand/Shortest_or_Optimal_Path_Routing#Usage_Examples "wikilink") for more information on turning trips into routes.

### How do I maintain a constant number of vehicles in the net?


There are different methods for accomplishing this. In either case the simulation itself should be constraint using options .

-   You can use the option to set the desired number. Vehicle insertions are delayed whenever this number would be exceeded. To avoid a large number of delayed vehicles it is recommended to also use the option . When using this approach you must ensure that there is a sufficient number of vehicles that are ready for insertion at all times. Note, that the number of distinct vehicle IDs over the whole simulation is much larger the specified value because some vehicles leave the simulation and new vehicles with distinct IDs are inserted to replace them.

-   You can use [rerouters](/Simulation/Rerouter "wikilink") in the simulation. Rerouters, assign a new route for vehicles driving across them and thus prevent them from leaving the network. For an example with a simple circle see
    -   If the networks is not circular to begin with (i.e a single road) you can make the network circular in a non-geometrical way by adding a return edge and declaring it's length to be very short (minimum 0.1m).
-   You can generate long trips going around the network with lots of detours. This can be accomplished using [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") by setting the options below. If the network contains disconnected parts, not all random trips will be viable. In this case, simply generate more trips and delete superfluous vehicles from the output route file.
    -   <your desired begin time>

    -   <begin + time in which vehicles shall be inserted to then network>

    -   &lt;(end - begin) / number of vehicles desired&gt;

    -   set to a large value to ensure that vehicles remain in the simulation long enough

    -   <output route file>

### A vehicle cannot reach its target or takes a circuitous route. Why?


Unexpected routes are often caused by invalid lane-to-lane connections or [-restrictions](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink"). Even if there are some lanes on every edge that permit the vehicle, they may not be connected. If the vehicle has the default type, it will ignore access restrictions and travel on all lanes. The [netcheck tool](/Tools/Net#netcheck.py "wikilink") can be used to visualize connectivity from a starting edge and to discover missing connections. It may be necessary to [delete some detour edges](/NETCONVERT#Edge_Removal "wikilink") from [the network](/Networks/Import/SUMO_Road_Networks "wikilink") to discover the relevant connectivity boundaries.

<!-- -->


To investigate connectivity [SUMO-GUI](/SUMO-GUI "wikilink") can be made to show lane-to-lane connections when customizing the visualization options for junctions. To investigate lane-permission issues, the menu option *Edit-&gt;Select lanes which allow...* can be used for visualizing selected permissions.

### How do I generate SUMO routes from GPS traces?


The answer largely depends on the quality of your input data mainly on the frequency / distance of your location updates and how precise the locations fit your street network. In the best case there is a location update on each edge of the route in the street network and you can simply read off the route by mapping the location to the street. This mapping can be done using the python sumolib coming with sumo, see [Tools/Sumolib\#locate_nearby_edges_based_on_the_geo-coordinate](/Tools/Sumolib#locate_nearby_edges_based_on_the_geo-coordinate "wikilink").

<!-- -->


This will fail when there is an edge in the route which did not get hit by a data point or if you have a mismatch (for instance matching an edge which goes in the “wrong” direction). In the former case you can easily repair the route using [DUAROUTER](/DUAROUTER "wikilink") with .

<!-- -->


For more complex cases (i.e. large temporal gaps or spatial errors) the problem is known as [Map Matching](https://en.wikipedia.org/wiki/Map_matching). Open source tools exist to facilitate this ([MatchGPX2OSM](http://wiki.openstreetmap.org/wiki/Routing/Travel_Time_Analysis/MatchGPX2OSM) [graphhopper](https://github.com/graphhopper/map-matching))

<!-- -->


To exactly reproduce high-resolution trajectories, it is possible to map exact vehicle locations (including lateral positioning) and also to move vehicles beyond the road space by using the [TraCI moveToXY function](/TraCI/Change_Vehicle_State#move_to_XY_.280xb4.29 "wikilink").

Simulation
----------

### How to simulate an accident

SUMO automatically detects [vehicle collisions](/Simulation/Safety#Collisions "wikilink"). Since the default model aims to be accident free, some effort must be taken to [create accidents](/Simulation/Safety#Deliberately_causing_collisions "wikilink").

Often, the effects of an accident are required instead of the accident itself. Without using [TraCI](/TraCI "wikilink") the following approaches may be useful:

:\# Let a vehicle halt on the lane for some time (see [Definition of Vehicles, Vehicle Types, and Routes\#Stops](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink")). This works quite nice for simulating accidents.

:\# Put a variable speed sign of the lane where the accident is meant to be and let it reduce the speed (see [Simulation/Variable Speed Signs](/Simulation/Variable_Speed_Signs "wikilink")). This method will reduce the throughput on the lane, but further dynamics will rather not fit to what one would expect from an accident situation.

:\# You may of course combine both approaches. Within a project we simulated traffic incidents by letting vehicles stop on one lane and reducing the speed on the other lanes.

:\# Alternatively, you may [close one or more of the lanes on an edge](/Simulation/Rerouter#Closing_a_Lane "wikilink")

:\# If you [close the whole edge, rerouting may be triggered as well](/Simulation/Rerouter#Closing_a_Street "wikilink")

:\# By setting the option , traffic jams may be created after a registered [collision](/Simulation/Safety#Deliberately_causing_collisions "wikilink").

### I have changed my network and now SUMO does not load it.


Actually, SUMO-networks are not meant to be edited by hand. You have to describe everything within your input properly and let NETCONVERT build your network. Editing networks by hand is very complicated and error-prone.

### How do I change the duration of cycles and phases?


use [NETEDIT](/NETEDIT#Traffic_Lights "wikilink")

### I can not see a vehicle moving in my simulation


There may be several reasons why you do not see the cars.

-   The simulation is not yet running (click the “play” button ([Image:play.gif](/Image:play.gif "wikilink")), see [SUMO-GUI\#Usage_Description](/SUMO-GUI#Usage_Description "wikilink"))
-   If your simulation area is too big, cars will not be displayed unless you zoom into the net. Cars are simply to small when looking from far away. To change this you may also set the option *Draw with constant size when zoomed out* (see [visualization settings for vehicles](/SUMO-GUI#Changing_the_appearance.2Fvisualisation_of_the_simulation "wikilink")).
-   The simulation is too fast so that all vehicles disappear before being seen. To avoid this, you may [increase the *Delay*-value](/SUMO-GUI#Usage_Description "wikilink") to slow down the simulation.
-   [You might have outdated graphic card drivers](/#SUMO-GUI_windows_and_buttons_appear_but_no_net.2Fcars_are_visible_.2F_Vehicles_are_not_visible_or_flicker_.2F_Roads_are_drawn_on_top_of_vehicles "wikilink")

### Different departure times with different time step size


Vehicles are entering the network earlier with decreasing time step lengths.

The reason for this behaviour is that a vehicle is emitted at the end of a time step. For one second time steps, this means that a vehicle which has the depart time of 0 will be inserted into the network at the end of the time step between 0 and 1, this means almost on second 1 (0.99...). If time steps of 0.1 seconds are used, the same vehicle is inserted into the network at the end of the time step between 0 and 0.1, this means almost on 0.1 (0.099...).

### How to save a simulation state and proceed later and/or differently


See [Simulation/SaveAndLoad](/Simulation/SaveAndLoad "wikilink")

### The simulation gets slow with many vehicles waiting for insertion


SUMO keeps checking continuously for possible vehicle insertions. If the network is jammed the number of necessary checks grows quickly. The option may be used to discard vehicles which could not be inserted within seconds.

### The simulation runs slow on the command line


when running on the windows operating system, the command-line output which is refreshed every simulation step slows the simulation down significantly. Use option to avoid this.

### The simulation has lots of jams/deadlocks. What can I do?

Deadlocks in a scenario can have many causes:

-   invalid network
    -   invalid lane numbers
    -   missing turning lanes
    -   invalid connections
    -   invalid junctions [(big clusters of small junctions should be joined)](/Networks/Building_Networks_from_own_XML-descriptions#Joining_Nodes "wikilink")
-   invalid traffic lights
-   invalid demand (too many vehicles overall, too many vehicles starting on the same edge, vehicles starting at inappropriate lanes)
-   invalid routing (only shortest path were used instead of [a user assignment algorithm](/Demand/Dynamic_User_Assignment "wikilink")

If the network was imported from OpenStreetMap, it is highly recommended to use the [recommended import options](/Networks/Import/OpenStreetMap#Recommended_NETCONVERT_Options "wikilink"). The best course of action typically is to observe the simulation using [SUMO-GUI](/SUMO-GUI "wikilink") and figure out where the first jam develops. If traffic lights are a cause of jamming, it can help to add the option when building the network. This generates [traffic-actuated systems](/Simulation/Traffic_Lights#Actuated_Traffic_Lights "wikilink") instead of static plans and usually improves performance.

### Why do the vehicles perform unexpected lane-changing maneuvers?


This may be caused by invalid lane-to-lane connections. Check the connections in [SUMO-GUI](/SUMO-GUI "wikilink") by activating *Junctions-&gt;show lane to lane connections* in the [gui settings dialog](/SUMO-GUI#Changing_the_appearance.2Fvisualisation_of_the_simulation "wikilink").

### How do I get high flows/vehicle densities?

The following parameters will allow flows in the range of 2500 vehicles/hour/lane

-   (needed to allow vehicles to catch up with their leader which is impossible if all drive at the same speed)

-

To increase flows even further the following settings can be used (potentially sacrificing some realism)

-   -   --step-length 0.5
-   (should not be lower than step-length)

### How do I force a lane change?


There are several options to force a vehicle onto a lane:

-   setting vehicle attributes ['departLane' and 'arrivalLane'](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#A_Vehicle.27s_depart_and_arrival_parameter "wikilink")
-   setting a [<stop>](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink") on the desired lane (also affects speed)
-   setting a route that requires lane-changing to a specific lane for continuation
-   setting the vehicle [class of the vehicle and forbidding that class from using the other lanes of an edge](/Simulation/VehiclePermissions "wikilink")
-   trigger the lane-change via [TraCI](/TraCI/Change_Vehicle_State#change_lane_.280x13.29 "wikilink")

### Are there any limits in regard to the size of a simulation scenario?

-   There are no hard limits on the number of streets, intersections or vehicles in SUMO. Make sure that you have enough RAM when trying to build or run scenarios beyond city-size. It may be necessary to use the 64bit version of SUMO to make use of available RAM.
-   The maximum length of a simulation scenario is 292 million years. If you need to simulate longer time periods you must [save and reload the simulation state](/#Save_a_simulation_state_and_proceed_later_and.2For_differently "wikilink")

Visualisation
-------------

### SUMO-GUI breaks


Sometimes [SUMO-GUI](/SUMO-GUI "wikilink") terminates with no reason. In most cases, an update of the opengl-driver solves this problem.

### Display flickers in the area of the mouse pointer (Windows)


Newer Windows-Versions seem to cache the area under the mouse to apply the mouse shadow afterwards. To avoid this, go to your Systemmenu, then Mouse-&gt;Pointers and disable the mouse shadows. That's the only solution so far. (Origin: Till Oliver Knoll, via QT Interest List)

### SUMO-GUI windows and buttons appear but no net/cars are visible / Vehicles are not visible or flicker / Roads are drawn on top of vehicles


This problem may occur when using outdated/wrong openGL drivers. Please try to update the drivers for you graphics hardware.

### Building videos from SUMO-GUI

There are several ways to build videos from your SUMO simulation. You can use screen capturing tools like VLC Player [1](http://www.videolan.org/vlc) or CamStudio [2](http://camstudio.org). The disadvantage of this approach is the requirement of a (very) fast CPU to capture the video in real time, it depends on the chosen resolution and screen size of the simulation.

Another approach is the use of single images for every simulation timestep. This can be done with an additional traci command for building screenshots. A small python snippet shows the usage of this TraCI command to get a new image for each new timestep.

    for i in range(duration):
        traci.simulationStep()
        traci.gui.screenshot("View #0", "images/"+str(i)+".png")

Next you have to glue the images together. This job can be done graphically with virtualdub [3](http://www.virtualdub.org) or via commandline with ffmpeg [4](http://www.ffmpeg.org). An example command for ffmpeg is shown below.

    ffmpeg -r 10 -i images/%d.png -b:v 1500k -vcodec wmv2 sumo.wmv

The parameters -r set the value for the fps and -b:v the bitrate for the video.

### Incomplete output

When using the GUI or TraCI the output files seem sometimes incomplete because the files are only flushed when everything is closed. For the GUI you can either use the close item from the menu or close the whole GUI. In TraCI it is always a good idea to wait for the sumo process to be finished using some kind of [process.wait()](https://docs.python.org/2/library/subprocess.html#popen-objects) mechanism

### Incompatibility with DisplayLink devices

Drivers of [DisplayLink](http://www.DisplayLink.com) devices are incompatibles with Fox Library. If SUMO or netEdit presents graphics problem like [this](http://sumo.dlr.de/wiki/File:DisplayLinkError.png) during the execution, DisplayLink drivers must be uninstalled.

Upgrading
---------

### How do I upgrade SUMO?


The easiest way is to download the latest sumo release to a directory of your choices and start using it from there. You may have to update the environment variables *PATH* and *SUMO_HOME* to ensure that the correct version of the application is called from the command line (see [Basics/Basic_Computer_Skills\#Configuring_Path_Settings](/Basics/Basic_Computer_Skills#Configuring_Path_Settings "wikilink")).

### [SUMO](/SUMO "wikilink") warns about deprecated networks or fails to load them


In major versions (whenever the 1st or 2nd digit of the version number changes) there may be changes to the network format. In this case we provide scripts in */tools/net* which can be used to upgrade your networks automatically. The current version of [NETCONVERT](/NETCONVERT "wikilink") can also be used to upgrade most network files to the current version. Simply call `netconvert -s `*`old.net.xml`*` -o `*`new.net.xml`*

Python tools
------------

### How do I run the python tools?


See [here](/Basics/Using_the_Command_Line_Applications#Using_Python_tools_from_the_Command_Line "wikilink")

### tools fail with a SyntaxError or ImportError or some TypeError concerning “&gt;&gt;”


Many python tools require python version 2.7. We aim to have Python 3 compatibility for [sumolib](/Tools/Sumolib "wikilink") and [traci](/TraCI/Interfacing_TraCI_from_Python "wikilink") however.

### tools fail with an ImportError


Make sure to set the environment variable SUMO_HOME to point at the base directory of your SUMO installation (the directory that contains *tools* and *bin*).

### how do I import [traci](/TraCI/Interfacing_TraCI_from_Python "wikilink") or [sumolib](/Tools/Sumolib "wikilink") in my own python script?

In order to import these libraries the folder /tools must be in your [python search path](https://docs.python.org/2/tutorial/modules.html#the-module-search-path). This can be accomplished by modifying the python variable **sys.path** as explained [here](/TraCI/Interfacing_TraCI_from_Python "wikilink") and [here](/Tools/Sumolib "wikilink"). Alternatively you can hard-code the path to your SUMO-installation into your script:

` import sys`
` sys.path.append('/your/path/to/sumo/tools')`
` import traci`
` import sumolib`

### the python scripts do not accept command line arguments (windows only)

This is a [known issue](https://stackoverflow.com/questions/2640971/) with some python installations. The usual workaround if you are not allowed to do edit the registry, is to call the python interpreter explicitly, e.g. instead of

` script.py `<argument>

you do

` python script.py `<argument>

(Communication) Network Simulators
----------------------------------

### How do I use *.tcl* files with NS2?


Questions regarding NS2 should be put to [the NS2 mailing list](http://www.isi.edu/nsnam/ns/ns-lists.html).

### How do I combine SUMO with a network simulator?


Check out [veins](http://veins.car2x.org/).

Outdated (Questions for very old versions of SUMO)
--------------------------------------------------

### Vehicles do not drive on the last edge of their route


Up to (and including) version 0.13.1 a vehicle finished its route (per default) on position 0 of the last edge. You can change this by setting the attribute **departPos** in the vehicle definition (see [Definition_of_Vehicles,_Vehicle_Types,_and_Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink")). Negative values count backwards from the end of the edge, thus setting **departPos**=“-1” will make the vehicle drive (almost) to the end of the last edge. The new default in more recent versions is the end of the edge, which should disable this behavior.

### Vehicle jumps backward


When I try to evaluate my vehicle dump, sometimes vehicle seem to jump backward (their position is smaller than in the previous step)

<!-- -->


To avoid jams due to an inappropriate lane changing behavior, vehicles may swap their lanes. In this case each vehicle obtains the position and speed of the other vehicle. As the position of the vehicles may differ a bit, one of the vehicles may seem to jump backwards.

<!-- -->


This should not happen from Version0.8 on.