---
layout: post
title: Installing MacOS Build w Homebrew
permalink: /Installing/MacOS_Build_w_Homebrew/
---

If you come from a previous macports installation you need to uninstall sumo and fox toolkit first:

` sudo port uninstall sumo`
` sudo port uninstall fox`

If you did not already install [homebrew](http://brew.sh) do it by invoking

`ruby -e `“`$(curl`` ``-fsSL`` `[`https://raw.githubusercontent.com/Homebrew/install/master/install`](https://raw.githubusercontent.com/Homebrew/install/master/install)`)`”

make sure your homebrew db is up-to-date

`brew update`

Install dependencies

`brew install Caskroom/cask/xquartz`
`brew install autoconf`
`brew install automake`
`brew install pkg-config`
`brew install libtool`
`brew install gdal`
`brew install proj`
`brew install xerces-c`
`brew install fox`

Set necessary environment variables

`export CPPFLAGS=`“`$CPPFLAGS`` ``-I/opt/X11/include/`”
`export LDFLAGS=`“`-L/opt/X11/lib`”

[Get the source code](/Installing/Linux_Build#Getting_the_source_code "wikilink") and change to the appropriate directory

`cd sumo-`<version>

Run autoreconf

`autoreconf -i`

Run configure

`./configure CXX=clang++ CXXFLAGS=`“`-stdlib=libc++`` ``-std=gnu++11`”` --with-xerces=/usr/local --with-proj-gdal=/usr/local`

Build

`` make -j`sysctl -n hw.ncpu` ``

Install

`make install`

After the installation you need to log out/in in order to let X11 start automatically, when calling a gui-based application like “sumo-gui”. (Alternatively, you may start X11 manually by pressing *cmd-space* and entering “XQuartz”).