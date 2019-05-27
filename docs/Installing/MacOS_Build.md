---
layout: post
title: Installing MacOS Build
permalink: /Installing/MacOS_Build/
---

__FORCETOC__

Using Macports
==============

You should start by [installing Macports](https://www.macports.org/install.php). Afterwards start a terminal session and run

`sudo port install sumo`

While this will install a SUMO version you maybe do not want to use, it will pull in all dependencies you need.

If you want to build from a repository checkout you should additionally do

`sudo port install automake autoconf`

After obtaining the [required libraries](/Installing/Linux_Build#Installing_required_tools_and_libraries "wikilink") you can follow the build steps of [building under Linux](/Installing/Linux_Build#Getting_the_source_code "wikilink"), you might want to add another --prefix=/opt/sumo to the configure line.

If you wish to use clang rather than gcc for compilation do:

`./configure CXX=clang++ CXXFLAGS=`“`-stdlib=libstdc++`”

Thanks to all MacOS builders for sharing their insights.

Using Homebrew
==============

By building SUMO from sources you can be sure to make use of the latest version. For detailed instructions see [building with Homebrew](/Installing/MacOS_Build_w_Homebrew "wikilink"). There is also a [Homebrew recipe](https://github.com/Homebrew/homebrew-science/blob/master/sumo.rb).