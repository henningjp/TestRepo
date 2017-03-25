# Wrapper of IF97 for MathCAD 15 and Mathcad Prime

This wrapper will provide User Defined (Custom) Functions in Mathcad 15 (or Prime) that provide thermodynamic and transport properties for water/steam at specified state points based on the IAPWS Industrial Formulation for the Properties of Water and Steam.  While these properties can also be accessed through the CoolProp add-in, this wrapper provides **_only_** these properties without the overhead of CoolProp.

This wrapper been developed and tested on Mathcad 15.0 (any maintenance release) and Mathcad Prime 3.0/3.1.  It May work on earlier versions of Mathcad and Mathcad Prime, but it has not been tested there.

## To Use

* Compile in VS2010 or later using the solution and project files (see below)

* Copy the if97.dll file to C:\\Program Files (x86)\\Mathcad\\Mathcad 15\\userefi or equivalent for your version (this will be done automatically by the project)  
  
* Copy the IF97_EN.xml to C:\\Program Files (x86)\\Mathcad\\Mathcad 15\\doc\\funcdoc.  Functions and descriptions will then be available in the Mathcad 15 interface under Insert|Function or the Functions button on the toolbar.

* View if97_verification.xmcdz or if97_verification.pdf for examples of using the functions.

## To Build

### Pre-Requisites

* You will need to have at least Visual Studio 2008 installed (Express version is fine).  Alternatively newer versions of Microsoft Visual Studio C++ should be fine; Builds have be tested on Visual Studio 2010 and 2015.
* You will need CMake version 2.8.12 or later from https://cmake.org/download/
* You will need to install Git-SCM for Windows.  You can install this from https://git-for-windows.github.io

### Download the IF97 Repository

* Open a Git window at the drive location where you want to create your local IF97 repository

* Clone the CoolProp/IF97 library to a local repository (If you haven't already cloned it recursively with CoolProp).::

    git clone https://github.com/CoolProp/IF97

* Change directory (cd) to the IF97 directory you just created.::

    cd IF97

### Building for Mathcad 15

* **Go to the top level CoolProp directory and make a build directory** (something like \build15)::

    mkdir build15 
    cd build15

* **Build the makefile using CMake** (Note: Mathcad 15 is 32-bit)::

    cmake .. -DCOOLPROP_MATHCAD15_MODULE=ON 
             -DCOOLPROP_MATHCAD15_ROOT="C:/Program Files (x86)/Mathcad/Mathcad 15"  
             -G "Visual Studio 10 2010" 
             -DCMAKE_VERBOSE_MAKEFILE=ON 

* **Make the dynamic library (DLL)**::

    cmake --build . --config Release



## Installing

* Build the if97 DLL in Visual Studio.  The project will automatically copy the DLL and function documentation to the appropriate Mathcad installation directory.  You may have to allow user write access to both:

	``C:\Program Files (x86)\Mathcad\Mathcad 15\userefi``
	
    and
		
	``C:\Program Files (x86)\Mathcad\Mathcad 15\doc\funcdoc``

* Follow the above instructions for use.

## Compiler Flags

The Mathcad wrapper code uses the ``REGION3_ITERATE`` flag to provide more accurate (but slightly slower) calculation of density in Region 3 (mostly super-critical) and does not use the ``IAPWS_UNITS`` flag, leaving all input/output values in SI units.
