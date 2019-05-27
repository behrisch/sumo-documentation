---
layout: post
title: Developer Unit Tests
permalink: /Developer/Unit_Tests/
---

Introduction
============

The Unit Tests for SUMO are carried out with the help of the Framework [Google Test](http://code.google.com/p/googletest/). With *Google Test* new Unit Tests can be simple added or existing tests extended. All available tests are executed daily and it is checked whether these tests run through successfully. This installation guide is for the version 1.4.0 to 1.6.0 of *Google Test*.

Windows Setup
=============

After downloading open the project file *gtest-md.sln* in the directory *msvc* from Google Test in Visual Studio and build it. This works at least up to gtest 1.6.0 but may not work with newer versions because Google Test is switching to cmake. In the next step create an Windows environment variable GTEST that points to the installation directory of Google Test.

Open the Visual Studio project file *unittest* from the SUMO directory *\\unittest\\build\\msvc10*. You will need at least gtest 1.5.0 to work with Visual Studio 2010. You can extend available tests or write new tests. Should you start a new Unit tests project the following settings in Visual Studio have to be made:

-   “..\\unittests.vsprops” must be added to Project -&gt; Properties -&gt; Configuration -&gt; General -&gt; Inherited Project Property Sheets.

<!-- -->

-   “$(GTEST LIB) $(GTEST DEBUG LIB)” must be added to Project -&gt; Properties -&gt; Configuration -&gt; Linker -&gt; Input -&gt; Additional Dependencies.

<!-- -->

-   The required Visual studio projects from the directory *build* under SUMO must be added and a dependence to these projects must be defined.

<!-- -->

-   Finally the class with the Main method is added, for example unittest_main.cpp from the directory unittest/src.

Linux setup
===========

After downloading you have to executed the following commands in the Google Test directory:

`./configure`
`make`
`sudo make install`

Now all libraries are installed in the system directory /usr/local or /usr/bin. Before the Unit Tests can be executed, you must build SUMO with an additional input parameter:

`./configure --with-gtest=DIR (DIR=installation directory of GoogleTest)`

If new Unit Test files are added under *unittest/src*, the Makefiles must be updated in order to run all tests.