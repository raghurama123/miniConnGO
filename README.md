# miniConnGO

! How to compile?
! ---------------
! gfortran miniConnGO.f90 -o miniConnGO.x
!
! How to run? 
! -----------
! ./miniConnGO.x    mol1_obabel.sdf    mol1_orca.out    mol1_orca.sdf
!                   ( argument-1 )     ( argument-2 )   ( argument-3, optional )  
!
! Two input files are required and must be kept in the same location the program is executed: 
! 1. mol1_obabel.sdf     <-- an SDF file (for example generated with obabel)
! 2. mol1_orca.out       <-- Output file from an Orca run of geometry optimization
!
! The names of these files form argument-1 and argument-2 
!
! Optionally, a third argument may be provided containing the file name
! to collect the geometry from the Orca output in the SDF format using connectivities
! from 'argument-1'
