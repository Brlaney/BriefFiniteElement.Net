## Validation and Testing
In a FEM application, which can have a very complicated code dependency graph (for example a method is called several times from several places) it is a vital thing, beacause making mistake in placing a positive instead of a negative sign in a mathematics formula  
will almost always change the result to something other than expected.

This library is developed regarding "Code Reuse" so the code will be somehow complicated. There are several types of validation for FE models in this library:

	- Unit Test (or integral test) (in project ``BriefFiniteElementNet.Tests``)
	- Validating the result with OpenSees (the Open System for Earthquake Engineering Simulation) available at [opensees.berkeley.edu](http://opensees.berkeley.edu/)
	- Validating the result with Frame3dd application available at [frame3dd.sourceforge.net](http://frame3dd.sourceforge.net)

	for more information on validation please have a look at [Validation.md](Validation.md) file.

## Unit Tests
Unit test is a test for very basic units of an application. For this library, there are several unit test implemented consist of:

- Mostly for checking effect of different loads (like uniform, concentrated or nonuniform) on BarElement

Unit tests implemented here are not so unit test, and somehow they can be called integral test as each unit test here is engaging more than one method in library.

Unit Test are located in project ``BriefFiniteElementNet.Tests``, and they will be validated on each push and if any fail, appveyor icon here (or in main readme.md file) will show the fail:
[![Build status](https://ci.appveyor.com/api/projects/status/q5an94f88kofefm9?svg=true)](https://ci.appveyor.com/project/epsi1on/bfe-net)  
If it is showing the 'Passing' then unit tests are good.

## Validate result with other well known applications
Two other applications are used for validation, 

*  Validating the result with OpenSees (the Open System for Earthquake Engineering Simulation) available at [opensees.berkeley.edu](http://opensees.berkeley.edu/)
*  Validating the result with Frame3dd application available at [frame3dd.sourceforge.net](http://frame3dd.sourceforge.net)

To validate output result with OpenSEES software we should convert model into TCL command format, then feed it into opensees.exe and extract result and check with BFE output. This procedure can be automatically done with codes already in `BriefFiniteElementNet.Validation.Ui` which is a console project. This is a comparison between results of BFE and OpenSEES for a simple 3d grid containing `BarElement` with a random load (force+moment) applied to each of the nodes:

!(Simple 3D Grid)[Simple3DGrid.png]
!(Simple 3D Grid - With Loads)[Simple3DGrid-withloads.png]

Result:

Maximum Absolute Difference in Nodal Displacements: 
Average Nodal Displacemenet:
Maximum Absolute Difference in Support Reactions: 
Average Support Reaction:

opensees input tcl file: [validation1.in.tcl](validation1.in.tcl) 
opensees output xml file: [validation1.out.xml](validation1.out.xml)