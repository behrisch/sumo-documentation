---
layout: post
title: Installing Linux Build
permalink: /Installing/Linux_Build/
---

This document describes how to install SUMO on Linux from sources. If you don't want to **extend** SUMO, but merely **use** it, you might want to [download one of our pre-built binary packages](/Installing "wikilink") instead.

To be able to run SUMO on Linux, just follow these four steps:

1.  Install all of the required tools and libraries
2.  Get the source code
3.  Build the SUMO binaries
4.  Install the SUMO binaries to another path (optional)

Each of these steps is outlined below.

Installing required tools and libraries
---------------------------------------

-   For the build infrastructure you will need a moderately recent g++ (4.8 will do) or clang++ together with the autotools (autoconf / automake).
-   The libraries needed are the Fox Toolkit in version 1.6.x, Xerces-C, Proj and GDAL. To compile you will need the devel versions of all packages. For openSUSE this means installing libxerces-c-devel, libproj-devel, libgdal-devel, and fox16-devel. There are some [platform specific and manual build instructions for the libraries](/Installing/Linux_Build_Libraries "wikilink")
-   Optionally you may want to add ffmpeg-devel (for video output), libOpenSceneGraph-devel (for the experimental 3D GUI) and python-devel (for running TraCI pythons scripts without a socket connection)

Getting the source code
-----------------------

### release version or nightly tarball

Download \[<http://prdownloads.sourceforge.net/sumo/sumo-src-%7B%7BVersion%7D>}.tar.gz?download sumo-src-.tar.gz\] or <http://sumo.dlr.de/daily/sumo-src-git.tar.gz>

`tar xzf sumo-src-`<version>`.tar.gz`
`cd sumo-`<version>`/`

### repository checkout

The following commands should be issued:

`git clone --recursive `[`https://github.com/eclipse/sumo`](https://github.com/eclipse/sumo)
`cd sumo`
`git fetch origin refs/replace/*:refs/replace/*`

The additional fetch of the replacements is necessary to get a full local project history.

### Definition of SUMO_HOME

Before compiling is advisable (essential if you want to use Clang) to define the environment variable SUMO_HOME. Assuming that you placed SUMO in the folder “*/home/<user>/sumo-<version>*”, if you want to define only for the current session, type in the console

`export SUMO_HOME=`“`/home/`<user>`/sumo-`<version>”

If you want to define for all sessions (i.e. for every time that you run your Linux distribution), go to your HOME folder, and find one of the next tree files (depending of your Linux distribution): **.bash_profile**, **.bash_login** or **.profile** (Note that these files can be hidden). Then edit the file, add the line from above at the end and restart your session.

You can check that SUMO_HOME was successfully set if you type

`echo $SUMO_HOME`

and console shows “/home/<user>/sumo-<version>”

Building the SUMO binaries with autotools
-----------------------------------------

To build from a checkout the [GNU autotools](http://en.wikipedia.org/wiki/GNU_build_system) are needed. The call to the autotools is hidden in Makefile.cvs.

`make -f Makefile.cvs`

`./configure [options]`
`make`

If you built the required libraries manually, you may need to tell the configure script where you installed them (e.g. **--with-xerces=...**). Please see the above [instructions on installing required tools and libraries](/Installing/Linux_Build_Libraries "wikilink") to find out how to do that.

Other common options to ./configure include **--prefix=$HOME** (so installing SUMO means copying the files somewhere in your home directory), **--enable-debug** (to build a version of SUMO that's easier to debug), and **--with-python** which enables the direct linking of python.

For additional options please see

`./configure --help`

After doing **make** you will find all binaries in the bin subdir without the need for installation. You may of course do a make install to your intended destination as well, see below.

### Building with clang

If you want to use a different compiler (just for the fun of it or because it has additional features) you can enable it at configure time. Our current clang configuration for additional static code checking looks like this:

`./configure CXX=clang++ CXXFLAGS=`“`-stdlib=libstdc++`` ``-fsanitize=undefined,address,integer,unsigned-integer-overflow`` ``-fno-omit-frame-pointer`` ``-fsanitize-blacklist=$PWD/build/clang_sanitize_blacklist.txt`”

You may of course leave out all the sanitizer-checks you don't want but the stdlib option has to be set. The blacklist filters out a known bug in the cstdlib. For details see the clang documentation.

### Additional notes for Cygwin users

At the moment GUI building is still troublesome. It depends whether you want to use the X-Server or native Windows GUI. We tried native Windows GUI only and had to change the installed libFOX-1.4.la such that it contains

`dependency_libs=' -lgdi32 -lglaux -ldl -lcomctl32 -lwsock32 -lwinspool -lmpr`
`-lpthread -lpng /usr/lib/libtiff.la /usr/lib/libjpeg.la -lz -lbz2 -lopengl32 -lglu32'`

Your mileage may vary.

Building the SUMO binaries with cmake
-------------------------------------

To build with cmake version 3 or higher is required.

Create a build folder for cmake (in the sumo root folder)

` mkdir build/cmake-build`
` cd build/cmake-build`

then build sumo with the bare minimum of options use (fully EPL2 compatible):

` cmake ../..`

after this is finished, run

` make`

to use additional features (gdal, gl2ps,...) set another option when building:

` cmake  -D CHECK_OPTIONAL_LIBS=true ../..`

Installing the SUMO binaries
----------------------------

This (optional) step will copy the SUMO binaries to another path, so that you can delete all source and intermediate files afterwards. If you do not want (or need) to do that, you can simply skip this step and run SUMO from the bin subfolder (bin/sumo-gui and bin/sumo).

If you want to install the SUMO binaries, run

`make install`
` `

Troubleshooting
---------------

### Problems with aclocal.m4 and libtool

If you're experiencing problems with aclocal.m4 definitions and see

` `“`You`` ``should`` ``recreate`` ``aclocal.m4`”

during the build, you should run the following commands:

`aclocal`
`libtoolize --force`
`autoheader`
`autoconf`
`./configure [your configure options]`
`make [install]`

### Unresolved references to openGL-functions

Build reports unresolved references to openGL-functions, saying things such as

`"./utils/glutils/libglutils.a(GLHelper.o): In function`
`` `GLHelper::drawOutlineCircle(float, float, int, float, float)': ``
`/home/smartie/sumo-0.9.5/src/utils/glutils/GLHelper.cpp:352:`
`` undefined reference to `glEnd'" ``

SUMO needs FOX-toolkit to be build with openGL-support enabled. Do this by compiling FOX-toolkit as following:

`tar xzf fox-1.4.34.tar.gz`
`cd fox-1.4.34`
`./configure --with-opengl=yes --prefix=$HOME && make install`

------------------------------------------------------------------------

**Further comment from Michael Behrisch (\[sumo-user\], 4.4.2007):** *Probably there is something wrong with your OpenGL installation. Make sure you have the libGL.so and libGLU.so which are most likely symbolic links to libGL.so.1.2 or something like this. They should appear in /usr/lib and case does matter (so “libgl.so” won't do).*

### Problems with the socket subsystem

Problem:

`recv ./foreign/tcpip/libtcpip.a(socket.o)  (symbol belongs to implicit dependency /usr/lib/libsocket.so.1)`

Solution: <http://lists.danga.com/pipermail/memcached/2005-September/001611.html>

### ld cannot find an existing library (Fedora-23)

Problem:

`/usr/bin/ld: cannot find -lfreetype`
`ls -lah /usr/lib64/libfreetype*`
` lrwxrwxrwx. 1 root root   21 Jul 28 15:54 /usr/lib64/libfreetype.so.6 -> libfreetype.so.6.12.0`
` lrwxr-xr-x. 1 root root 689K Jul 28 15:54 /usr/lib64/libfreetype.so.6.12.0`

Solution: Install the dev package; for fedora:

`sudo yum install freetype-devel`

For details see [stackoverflow](http://stackoverflow.com/questions/335928/ld-cannot-find-an-existing-library) discussion.