---
layout: post
title: Developer Tests
permalink: /Developer/Tests/
---

Introduction
============

We use [TextTest](http://texttest.org/) to test whether the software still behaves as expected. What [TextTest](http://texttest.org/) does is to compare an application's output, including the output to stdout, stderr, and into generated files with predefined outputs from files.

There are some advantages and disadvantages of this approach. On the one hand, you can guarantee that the application is doing what is wanted by comparing all outputs with files you think are right. But this is also the problem with this approach: you do not have the assurance that the files you are comparing the current outputs to ARE right - you have to prepare them once and update/verify them again everytime the expected results change.

Setup
=====

We use [TextTest](http://texttest.org/) as our testing environment which is python based. To install it, you can open a Terminal/Windows console and type:

`pip install texttest`

on all platforms but it will not pull in the dependencies, so you need to follow the [texttest installation instructions](http://texttest.org/index.php?page=documentation_trunk&n=install_texttest) and the additional info here.

Windows Setup
-------------

You will need the following software (at least for a setup with GUI)

-   [Python 2.7](http://www.python.org/download/)
-   [GTK and PyGTK for Windows](http://www.gtk.org/download/)
    -   If you are using the 32 bit version of Python you can use [the all in one installer](http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.24/pygtk-all-in-one-2.24.0.win32-py2.7.msi)
    -   For 64 bit this <http://stackoverflow.com/questions/14567921/python-pygtk-windows-7-64-bit> answer still applies except that the unofficial python packages now need pip to be installed
-   [TKDiff](http://tkdiff.sourceforge.net/) (you can choose another compatible diff tool if you like)
-   python and diff should also appear in your PATH.

Visual guide:

Image:TestInstall1.png|Python path shouldn't include whitespaces Image:TestInstall2.png|Python requieres a full installation Image:TestInstall3.png|PyGTK must be installed in the same folder of Python

Image:TestInstall6.png|TkDiff path shouldn't include whitespaces Image:TestInstall4.png|Check that python works typing “Python” in CMD. Type “quit()” to exit Image:TestInstall5.png|Type *pip install texttest* to install TextTest automatically from Python repository

Image:TestInstall7.png|Every value of environment variable “PATH” must be separated with “;” Image:TestInstall8.png|If Installation was successfully, this window will appear after execution of “runAllTests.bat”

Linux setup
-----------

This is much easier because at least with recent distributions there is probably everything included. With openSUSE 10.2 you need python-gtk and python-cairo as well as tkdiff before installing TextTest. If you don't need the GUI you can probably even skip these.

MacOS setup
-----------

You should use Macports and install py27-pip and the py27-pygtk package. If you install texttest via pip (use /opt/local/bin/pip, not the regular one) then, you will find the texttest executable in /opt/local/Library/Frameworks/Python.framework/Versions/2.7/bin/. If the run complains about an undefined locale set the following environment:

`export LC_ALL=C`
`export LANG=C`

Running the Tests
=================

Within the '' /tests'' - folder you can find batch-files which start [TextTest](http://texttest.org/) with our test suites. “runAllTests.bat” starts TextTest for testing all apllications located in the folder, “runNetconvertTests.bat” will only show tests for NETCONVERT, “runDuarouterTests.bat” only those for DUAROUTER etc.

Adding a Test to an existing Application
========================================

The easiest method is probably to copy an existing test using the Texttest GUI context menu functions (copy/paste). Then you can modify the copied input files, run the test once and save the expected results. Note, that input files may be picked up along the folder hierarchy so you may have to copy additional files to your test folder manually if these inherited input files must be changed as well.

Adding an Application Test Suite
================================

To add a test suite for a new application, you have to perform the following steps. For the examples below we'll use “polyconvert” as the example application.

-   go to '' {SUMO}/tests ''
-   copy one of the **run...Tests.bat**-files and rename it properly (**runPolyconvertTests.bat** in our case); change the name of the application within it. In our case the resulting file will look as this:

`call testEnv.bat`
`texttest.py -a polyconvert -gx`

-   add the application to the list of applications that are tested each night by
    -   adding it to **runTest.sh**; in our case, the following line was added:

`export POLYCONVERT_BINARY=`“`$SUMO_BIN/polyconvert`”

-   -   adding it to **testDaily.sh**; in our case, the following line was added:

`export POLYCONVERT_BINARY=`“`$SUMO_BIN/polyconvert`”

-   -   adding it to **testEnv.bat**; in our case, the following line was added:

`set POLYCONVERT_BINARY=%CD%\..\bin\polyconvert.exe`

-   build a test folder for the application, named as the application itself (without the “.exe” extension), in our case the folder is named **polyconvert**
-   go the folder
-   build a configuration file; its name is “config”, the extension is the application's to test name, so in our case it's **config.polyconvert**. Please consult [TextTest](http://texttest.org/) documentation about the content, nonetheless, here are some notes
    -   do not forget the import of the config file
    -   name the binary correct
    -   name the file name properly in output
    -   In all files that are collated, *Version* shold be ignored - the tests should be working along all versions


The initial file looks as following:

`import_config_file:../config_all`
`binary:$POLYCONVERT_BINARY`
`copy_test_path:input_net.net.xml`
`[collate_file]`
`config:config.cfg`
`log:log.txt`
`[run_dependent_text]`
`output:polyconvert.exe{REPLACE sumo-polyconvert}`
`net:Version`

-   build a top-level testsuite file; its name is “testsuite”, the extension is the application's to test name, so in our case it's **testsuite.polyconvert**
    -   I suppose, it is a good idea to start with tests of meta-output; Simply copy them from another application and patch the file names...

Example of use
==============

The main function of existing test is to verify that a modification of a function does not affect the final output, comparing the output of our modification in SUMO with a with an previously tested *output control file*. Note that **SUMO must be compiled in release mode for testing**. To show an example of use, the *MSDevice_Battery.cpp* file will be modified to include an error in the output file *battery.xml*. Once modified the line, run executable *runSumoTests.bat* and find the test *sumo/extended/electric/braunschweig*, and then right click to run the test

Image:TestError1.png|Manual error Image:TestError2.png|Running test

After execution can be observed that the *battery.sumo* file is marked in red. That means that the execution of our SUMO modification generated a different battery output than expected. If the file marked in red was *errors.sumo*, it means that our modification of SUMO has caused a *runtime error*, and finally if the file marked in red is *output.sumo*, it means that SUMO generated some warning during execution. Double-clicking on the red box *battery.sumo* opens ''TkDiffv automatically, and displays the differences of our battery output with respect to the original *battery output control file*.

Image:TestError3.png|Error in battery.sumo Image:TestError4.png|Detail of the error comparing both battery.sumo

At this point, we undone the modification in *MSDevice_battery.cpp* which caused the error, and compile. Once compiled, we will again right click over the failed text and press *rerun*. A new dialog will be opened, and then click over *Accept*, and test will be repeated. After the new test run no error is displayed.

Image:TestError5.png|Undo error Image:TestError6.png|Repeating test

After clicking on the check box next to the green message *Succeeded* can be observed that all output shown in green, and at the bottom appear a message indicating that the test has been succeeded.

Image:TestError7.png|Test succeeded Image:TestError8.png|Details of the test succeeded

Organization of Tests
=====================

Our Texttest tests can be grouped into 3 categories described below

Application Tests
-----------------

These tests are for the executable files in the *bin* folder such as [NETCONVERT](/NETCONVERT "wikilink"), [DUAROUTER](/DUAROUTER "wikilink") and [SUMO](/SUMO "wikilink"). They work by running their application once with a predefined set of input files and compare against expected output files.

Tool Tests
----------

These tests are for the python tools in the *tools* folder such as [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") and [flowRouter.py](/Tools/Detector#flowrouter.py "wikilink"). Instead of defining a new application for each tool (as is the stanard for TextTest) they all call the *tests/toolrunner.py* script and select the actual python tool to test via options.

Complex Tests
-------------

These tests go beyond calling an application once. Each tests defines a *runner.py* script which performs arbitrary application calls. This is used to call netconvert multiple times to perform back-and-forth format conversions or to test tutorials where first the network is generated and afterwards simualtion is performed. They are also used for testing the traci python client (runner.py is a traci script in this case).

Regular tests
=============

At the moment all our [tests run each night](http://sumo.dlr.de/daily/) on two linux machines of different age and on a windows server.