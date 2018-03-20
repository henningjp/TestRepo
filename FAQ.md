Frequently Asked Questions
==========================

Usage
-----

1. My enthalpy and entropy values are not the same as what are used in REFPROP, or EES, or ...

    Values for enthalpy, entropy and internal energy are calculated as *differences* 
    with respect to an arbitrarily chosen reference state. 
    As a consequence, absolute values may differ hugely between different tools, 
    but the difference between two states should be equal.  
    At least the following three states are frequently chosen as reference states:  
    IIR: saturated liquid (Q=0) at T=273.15 K  
    ASHRAE: saturated liquid (Q=0) at T=233.15 K  
    NBP: saturated liquid (Q=0) at p=101325.0 Pa
    
    
2. My calls to REFPROP fail with a mysterious `Segementation Fault`: 

    Make sure that you have at least REFPROP version 9.1 installed. If you have a license for 9.0, 
    the upgrade is for free: http://www.nist.gov/srd/nist23.cfm
    
3. Transport properties missing

    a. Fluid XY does not have viscosity/thermal conductivity/ ... 

       Please have a look at 
       http://www.coolprop.org/fluid_properties/PurePseudoPure.html#list-of-fluids 
       if there is no reference for your property, we do not have the information required to 
       implement the functionality. If you file an issue, please provide information and 
       a link to a publication with the required data. 
    
    b. ..but it used to work in an earlier version of CoolProp
    
       For some fluids, version 5 does not have transport properties even though version 4 had 
       that information. We decided to remove some correlations, which had very large uncertainties 
       and we would like to make the user aware of the fact that the old implementation was 
       experimental and results were not reliable at all.
    
Compilation
-----------

1. I'm on linux and I get compilation errors like

    ```
    gcc: error trying to exec 'cc1plus': execvp: No such file or directory
    error: Setup script exited with error: command 'gcc' failed with exit status 1
    ```
    
    This means that the g++ package is missing.  On OpenSUSE you can just install the following packages in software manager:
    
    ```
    gcc-c++
    gcc48-c++
    libstdc++48-devel
    ```
    
    On ubuntu, it should be sufficient to just run
    
    ```
    sudo apt-get install g++
    ```
    
2. Building Python wrapper on Windows fails with an error similar to

    ```
    error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": http://landinghub.visualstudio.com/visual-cpp-build-tools
    ```
    
    Different versions of Python (2.7, 3.6, etc.) are built with and require specific versions of the Microsoft Visual C++ compiler.  Please see the [common wrapper prerequisites](http://www.coolprop.org/dev/coolprop/wrappers/index.html#wrapper-common-prereqs) specifically for Windows build requirements.
    
    
    
    
    