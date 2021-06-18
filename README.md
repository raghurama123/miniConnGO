# miniConnGO

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fortran90](https://img.shields.io/badge/Language-Fortran90-red.svg)](https://en.wikipedia.org/wiki/Fortran)


Contains a fortran code to compare an SDF file and an output file of an Orca geometry optimization run.

# How to compile?

    gfortran miniConnGO.f90 -o miniConnGO.x


# How to run? 


    ./miniConnGO.x    argument-1     argument-2     argument-3 (optional) 

                   
Two input files are required and must be kept in the same location where the program is executed: 
1. mol1_obabel.sdf     <-- an SDF file (for example generated with obabel)
2. mol1_orca.out       <-- Output file from an Orca run of geometry optimization
Examples are given in the directory example

The names of these files form argument-1 and argument-2 

Optionally, a third argument may be provided containing the file name to collect the geometry from the Orca output in the SDF format using connectivities
from 'argument-1'
