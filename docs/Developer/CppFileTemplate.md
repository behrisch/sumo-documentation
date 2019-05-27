---
title: Developer CppFileTemplate
permalink: /Developer/CppFileTemplate/
---

`/****************************************************************************/`
`// Eclipse SUMO, Simulation of Urban MObility; see `[`https://eclipse.org/sumo`](https://eclipse.org/sumo)
`// Copyright (C) `<YEAR OF CREATION>`-`<CURRENT YEAR>` German Aerospace Center (DLR) and others.`
`// This program and the accompanying materials`
`// are made available under the terms of the Eclipse Public License v2.0`
`// which accompanies this distribution, and is available at`
`// `[`http://www.eclipse.org/legal/epl-v20.html`](http://www.eclipse.org/legal/epl-v20.html)
`// SPDX-License-Identifier: EPL-2.0`
`/****************************************************************************/`
`/// @file    `<FILENAME>
`/// @author  `<AUTHOR'S NAME, ONE SEPARATE LINE FOR EACH AUTHOR>
`/// @author  `<AUTHOR'S NAME 2>
`/// @author  `<AUTHOR'S NAME 3>
`/// @date    `<FILE CREATION DATE>
`/// @version $Id: $`
`///`
`/// `<A BRIEF DESCRIPTION OF THE FILE'S CONTENTS>
`/****************************************************************************/`
`// ===========================================================================`
`// included modules`
`// ===========================================================================`
`#ifdef _MSC_VER`
`#include <windows_config.h>`
`#else`
`#include <config.h>`
`#endif`
`#include `<StandardLibrary>`     // Standard libraries`
`#include `<SUMOLibrary>`         // SUMO libraries`
`#include `“`myHeaderFile1`”`       // Own libraries`
`#include `“`myHeaderFile2`”
`// ===========================================================================`
`// static member definitions`
`// ===========================================================================`
<parameterType>` OwnClass::myStaticMember = value;    // Define here values of static members`
`// ===========================================================================`
`// member method definitions`
`// ===========================================================================`
`OwnClass::OwnClass(`<parameterType>` parameter1, `<parameterType>` parameter2,... `<parameterType>` parametern) :`
`    parentClass(),             // Call to parent class (if inherit)`
`    myParameter1(parameter1),  // values of members should be inicializated with this method`
`    myParameter2(parameter1),`
`    ...`
`    myParametern(parametern) {`
`    // Code of constructor`
`}`
`OwnClass::~OwnClass() {}   // Declare always destructor, even if is empty`
`void `
`OwnClass::function() const {`
`    // code`
`}`
<parameterType>` `
`OwnClass::getParameter1() const {`
`    return myParameter1;`
`}`
`// ---------------------------------------------------------------------------`
`// Class::Subclass - methods `<LEAVE OUT IF METHODS ARE OF ONE CLASS ONLY>
`// ---------------------------------------------------------------------------`
`OwnClass::SubClass::SubClass() :`
`    myPrivateParameter(0) {`
`    // code of constructor`
`}`
`OwnClass::SubClass::~SubClass() {}`
`/****************************************************************************/`