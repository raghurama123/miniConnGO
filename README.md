# miniConnGO

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fortran90](https://img.shields.io/badge/Language-Fortran90-red.svg)](https://en.wikipedia.org/wiki/Fortran)


Contains a fortran code to compare an SDF file and an output file of an Orca geometry optimization run. A more elaborate package to perform Connectivity preserving Geometry Optimization is here: [ConnGO](https://github.com/raghurama123/ConnGO)

# How to compile?

    gfortran miniConnGO.f90 -o miniConnGO.x


# How to run? 


    ./miniConnGO.x     argument-1     argument-2     argument-3 (optional) 

                   
Two input files are required and must be kept in the same location where the program is executed: 

    1. mol1_obabel.sdf     <-- an SDF file (for example generated with obabel)
    2. mol1_orca.out       <-- Output file from an Orca run of geometry optimization
    
Examples are given in the directory example

The names of these files form argument-1 and argument-2 

Optionally, a third argument may be provided containing the file name to collect the geometry from the Orca output in the SDF format using connectivities
from 'argument-1'

# Sample execution

    raghurama$ gfortran miniConnGO.f90 -o miniConnGO.x
    raghurama$ ./conngo_test.x mol1_obabel.sdf mol1_orca.out mol1_orca.sdf

    == connectivities
                       File-1                  File-2                Deviation
    1  2  2  O = C     1.2201                  1.2153                  0.0048
    2  3  1  C - C     1.4729                  1.4656                  0.0073
    2  7  1  C - H     1.0858                  1.1188                 -0.0329
    3  4  2  C = C     1.3396                  1.3531                 -0.0134
    3  8  1  C - H     1.0872                  1.0937                 -0.0065
    4  5  1  C - C     1.4776                  1.4515                  0.0260
    4  9  1  C - H     1.0878                  1.0969                 -0.0091
    5  6  2  C = C     1.3351                  1.3448                 -0.0097
    5 10  1  C - H     1.0867                  1.0938                 -0.0071
    6 11  1  C - H     1.0861                  1.0931                 -0.0070
    6 12  1  C - H     1.0852                  1.0897                 -0.0046

    == bond lengths in file-1 in descending order, # ultralong bonds =    0
    1.4776    1.4729    1.3396    1.3351    1.2201    1.0878    1.0872    1.0867    1.0861    1.0858    1.0852

    == bond lengths in file-2 in descending order, # ultralong bonds =    0
    1.4656    1.4515    1.3531    1.3448    1.2153    1.1188    1.0969    1.0938    1.0937    1.0931    1.0897

    ** Geometries in file-1 and file-2 seem alright, no broken structures detected **

    == Mean square deviation of bond lengths from file-1 and file-2
    MSD  =     0.0146 Ang

    == Maximum absolute deviation in bond lengths from file-1 and file-2
    MaxAD=     0.0329 Ang

    == Mean percentage absolute deviation in bond lengths from file-1 and file-2
    MPAD =     0.9606

    == Outcome of the Connectivity preserving Geometry Optimization
    ** ConnGO PASS [MPAD < 5, MaxAD < 0.2 Angstrom] **
