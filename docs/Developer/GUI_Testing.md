---
layout: post
title: Developer GUI Testing
permalink: /Developer/GUI_Testing/
---

We are using [SikuliX](http://sikulix.com/)

Setup
-----

-   Java (at least 1.7) should be installed
-   Linux only: Install dependencies (openSUSE 42.1: `zypper in libopencv2_4 libtesseract3 wmctrl xdotool`)
    -   openSUSE 42.2 does not have libopencv2_4, you can try this libopencv2 from [this repo](https://build.opensuse.org/package/binaries/home:tokoyami/opencv2-qt5?repository=openSUSE_Leap_42.2) but you will need manual symlinks in /usr/lib64

`cd /usr/lib64/`
`ln -s libopencv_core.so.5.4 libopencv_core.so.2.4`
`ln -s libopencv_highgui.so.5.4 libopencv_highgui.so.2.4`
`ln -s libopencv_imgproc.so.5.4 libopencv_imgproc.so.2.4`

-   Download from [here](https://launchpad.net/sikuli/+download) and move the jar to a separate dir (e.g. $HOME/sikulix).
-   run setup `java -jar sikulix/sikulixsetup-1.1.0.jar`
    -   enable the first option and python scripting
-   Define environment variable, e.g. `export RUN_SIKULIX=$HOME/sikulix/runsikulix`
    -   on Windows `set RUN_SIKULIX=C:\sikulix\runsikulix.cmd`
-   see also <http://sikulix.com/quickstart/>

Startup
-------

-   run $SUMO_HOME/tests/runNeteditTests.sh (Linux) or %SUMO_HOME%\\tests\\runNeteditTests.bat (Windows)
    -   when getting an error about “server not running” double check whether the environment variable is set and try to run the script `RUN_SIKULIX` points to manually, looking for error messages.

Setting up a test
-----------------

All tests start are written in Python using the Jython scripting interface of Sikulix. All of them start with the same header:

`import os`
`import sys`
`testRoot = os.path.join(os.environ.get('SUMO_HOME', '.'), 'tests')`
`neteditTestRoot = os.path.join(os.environ.get('TEXTTEST_HOME', testRoot), 'netedit')`
`sys.path.append(neteditTestRoot)`
`import neteditTestFunctions as netedit`
`# Open netedit`
`neteditProcess, match = netedit.setupAndStart(neteditTestRoot, True)`

This code will find the directory with the netedit tests using the TEXTTEST_HOME variable and SUMO_HOME as a fallback. This enables the start of the tests even outside of Texttest using the runsikulix call directly with the test.sikuli dir. You should not use relative directories here because this makes copying and moving tests harder.