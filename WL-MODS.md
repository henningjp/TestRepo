# Enhancements to Original WL Package

These enhancements were added to the original RefpropLink package written by Wolfram Research for completeness and robustness.

1. Initialize paths to DLL and fluids folder automatically from `Filepaths.txt` when loading the RefpropLink package.  `Filepaths.txt` contains two comma separated strings: 

   - First string is the full path to the 64-bit DLL (e.g. "C:\Program Files (x86)\REFPROP\REFPRP64.DLL" (_default_))
   - Second string is the path to the location **_just above_** the \\fluids & \\mixtures folders (e.g. "C:\Program Files (x86)\REFPROP" (_default_)) 
   
2. Check validity of the DLL location and warn user if the DLL is not found. 

3. Make initial call to setup0[] when loading the RefpropLink package to retrieve the version of NIST Refprop version actually loaded.  Printed for information when package is loaded (or a warning that the REFPROP DLL was not found).  Needed to determine if new REFPROP 10 API functions should be loaded.

4. Added a public getversion[] function to simplify the above call and make it available to users. 

5. Remove [out] parameters from all legacy API function parameter list.  They were only used to pattern the .NET objects being used in the DLL call and were not returned.  Do not need to burden the user with these extra parameters.  Only the [in] parameters are supplied in the package functions.

6. While error code is returned from most functions in variable `ierr`, the error string in `herr` is not.  Instead, the `herr` string is printed directly after the function call if, and only if, `ierr > 0`.  This removes the need for the checkErrorCodes[] function and it has been commented out. 

7. Take any length array in the composition parameter.  Each function automatically trims and zero-pads the array to (`$ncmax = 20`) elements for consistency with the expected Fortran array length in the REFPROP DLL.

## To Do

- Check `LoadedNETObjects[]` to see what .NET objects are hanging around and if the list is growing (memory leak). 

- Use NETBlock[] if necessary on all functions that create NETObjects.  This will _Release_ these objects when returning from the function call to avoid memory leaks.
   ```Mathematica
   func[]:=
      NETBlock[
         Module[{loadXdll},
            (* Code here *)
         ]
      ]
   ``` 
   
- Pad all string NETObjects to their appropriate maxlength.  Ensures parameter alignment with the expected Fortran parameter strings at fixed lengths.  The .NET objects being used to pass the parameters back and forth from the DLL functions **_may_** already take care of thos, but we're doing it anyway to be sure.

