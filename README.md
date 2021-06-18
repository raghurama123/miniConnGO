# miniConnGO

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fortran90](https://img.shields.io/badge/Language-Fortran90-red.svg)](https://en.wikipedia.org/wiki/Fortran)


This program compares an SDF file and an output file of an Orca or Mopac geometry optimization run and reports if the atomic connectivity is preserved during geometry optimization. 

A more elaborate package to perform Connectivity preserving Geometry Optimization is here: [ConnGO](https://github.com/raghurama123/ConnGO)

# How to compile?

    gfortran miniConnGO.f90 -o miniConnGO.x


# How to run? 


    ./miniConnGO.x     argument-1     argument-2     argument-3     argument-4 (optional) 

                   
Two input files are required and must be kept in the same location where the program is executed: 

    1. mol1_obabel.sdf     <-- an SDF file (for example generated with obabel)
    2. mol1_orca.out       <-- Output file from an Orca/Mopac run of geometry optimization
    
Examples are given in the directories example_01 and example_02

The names of these files form argument-1 and argument-2 

Argument-3 is the name of the program used for geometry optimization. Accepted values are 'orca' or 'mopac'

Optionally, a fourth argument may be provided containing the file name to collect the geometry from the Orca output in the SDF format using connectivities
from 'argument-1'

# Sample execution - 1 
#### Obabel-UFF vs. Orca, see the directory example_01

    raghurama$ ./miniConnGO.x mol1_obabel.sdf mol1_orca.out orca mol1_orca.sdf
    
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
    
# Sample execution - 2 
#### Obabel-UFF vs. Mopac, see the directory example_02

    raghurama$ ./miniConnGO.x mol1_obabel.sdf mol1_mopac.out mopac mol1_mopac.sdf
    
    == connectivities
                       File-1                  File-2                Deviation
    1  2  2  O = C     1.2201                  1.2086                  0.0115
    2  3  1  C - C     1.4729                  1.4754                 -0.0025
    2  7  1  C - H     1.0858                  1.0985                 -0.0127
    3  4  2  C = C     1.3396                  1.3405                 -0.0009
    3  8  1  C - H     1.0872                  1.0905                 -0.0033  
    4  5  1  C - C     1.4776                  1.4582                  0.0193
    4  9  1  C - H     1.0878                  1.0943                 -0.0065
    5  6  2  C = C     1.3351                  1.3366                 -0.0014
    5 10  1  C - H     1.0867                  1.0928                 -0.0061
    6 11  1  C - H     1.0861                  1.0799                  0.0062
    6 12  1  C - H     1.0852                  1.0805                  0.0047
 
    == bond lengths in file-1 in descending order, # ultralong bonds =    0
    1.4776    1.4729    1.3396    1.3351    1.2201    1.0878    1.0872    1.0867    1.0861    1.0858    1.0852

    == bond lengths in file-2 in descending order, # ultralong bonds =    0
    1.4754    1.4582    1.3405    1.3366    1.2086    1.0985    1.0943    1.0928    1.0905    1.0805    1.0799

    ** Geometries in file-1 and file-2 seem alright, no broken structures detected **

    == Mean square deviation of bond lengths from file-1 and file-2
    MSD  =     0.0087 Ang

    == Maximum absolute deviation in bond lengths from file-1 and file-2
    MaxAD=     0.0193 Ang

    == Mean percentage absolute deviation in bond lengths from file-1 and file-2
    MPAD =     0.5657

    == Outcome of the Connectivity preserving Geometry Optimization
    ** ConnGO PASS [MPAD < 5, MaxAD < 0.2 Angstrom] **

# Sample execution - 3
#### MOPAC vs. Orca, using mol1_mopac.sdf from previous example

    raghurama$ ./miniConnGO.x mol1_mopac.sdf mol1_orca.out orca mol1_orca.sdf
        
    == connectivities
                       File-1                  File-2                Deviation
    1  2  2  O = C     1.2086                  1.2153                 -0.0067
    2  3  1  C - C     1.4754                  1.4656                  0.0098
    2  7  1  C - H     1.0985                  1.1188                 -0.0203
    3  4  2  C = C     1.3405                  1.3531                 -0.0126
    3  8  1  C - H     1.0905                  1.0937                 -0.0032
    4  5  1  C - C     1.4581                  1.4515                  0.0066
    4  9  1  C - H     1.0943                  1.0969                 -0.0026
    5  6  2  C = C     1.3367                  1.3448                 -0.0082
    5 10  1  C - H     1.0928                  1.0938                 -0.0010
    6 11  1  C - H     1.0799                  1.0931                 -0.0133
    6 12  1  C - H     1.0806                  1.0897                 -0.0092

    == bond lengths in file-1 in descending order, # ultralong bonds =    0
      1.4754    1.4581    1.3405    1.3367    1.2086    1.0985    1.0943    1.0928    1.0905    1.0806    1.0799

    == bond lengths in file-2 in descending order, # ultralong bonds =    0
      1.4656    1.4515    1.3531    1.3448    1.2153    1.1188    1.0969    1.0938    1.0937    1.0931    1.0897

    ** Geometries in file-1 and file-2 seem alright, no broken structures detected **

    == Mean square deviation of bond lengths from file-1 and file-2
    MSD  =     0.0100 Ang

    == Maximum absolute deviation in bond lengths from file-1 and file-2
    MaxAD=     0.0203 Ang

    == Mean percentage absolute deviation in bond lengths from file-1 and file-2
    MPAD =     0.7065

    == Outcome of the Connectivity preserving Geometry Optimization
    ** ConnGO PASS [MPAD < 5, MaxAD < 0.2 Angstrom] **
