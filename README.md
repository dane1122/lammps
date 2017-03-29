# LAMMPS compilation using Emscripten

LAMMPS is a powerful tool that allows scientists to simulate large-sclae molecules. However, the set-up for LAMMPS can be difficult for the first time users and you need to ensure that all the packages are installed in order to use it on your computer.

To resolve these limiting factors, Autodesk's BioNano group authored a series of __makefile__ with __step-by-step instructions__ to allow complilation of LAMMPS into __asm.js__ and __wasm__ using Emscripten. 

Emscripten is helping powerful C++ and C tools come into the web by compiling C++/C code into highly-optimizable JavaScript. This lets us run LAMMPS at near-native speed without additional plugins on the browser. To get started, just __clone this repository__ and __checkout our emscripten__ branch to get all the necessary files you need to compile LAMMPS into JavaScript.


## Our Contributions 

We had to modify/create our custom makefiles to successfully compile LAMMPS using Emscripten. The files that were changed/created are as below:

* [Modified the main Makefile](https://github.com/dane1122/lammps/blob/emscripten/src/Makefile)
* [Modified the stub Makefile](https://github.com/dane1122/lammps/blob/emscripten/src/STUBS/Makefile)
* [Created our custom Makefile for LAMMPS serial](https://github.com/dane1122/lammps/blob/emscripten/src/MAKE/MINE/Makefile.emcc-serial)
 
In addition, not all the packages that come with LAMMPS can be compiled into Emscripten *yet*. The packages we CAN compile as of now are:
> mpi-stubs, ASHPHERE, BODY, CLASS2, COLLOID, CORESHELL, DIPOLE, GRANULAR, KSPACE, MANYBODY, MC, MOLECULE, OPT, PERI, PYTHON, REPLICA, RIGID, SHOCK, SNAP, SRD


## Emscripten Compilation Guide 

Below are the step-by-step instructions on how to compile LAMMPS using Emscripten in MAC OSX: 

1. Get Emscripten on your computer: https://kripken.github.io/emscripten-site/docs/getting_started/downloads.html
2. Clone or download LAMMPS source code from __emscripten__ branch and `cd` into the `src` directory
3. Make the STUBS by entering `emmake make mpi-stubs` in terminal
4. Make the packages by entering `emmake make yes-ASPHERE yes-BODY yes-CLASS2 yes-COLLOID yes-CORESHELL yes-DIPOLE yes-GRANULAR yes-KSPACE yes-MANYBODY yes-MC yes-MOLECULE yes-OPT yes-PERI yes-PYTHON yes-REPLICA yes-RIGID yes-SHOCK yes-SNAP yes-SRD` in terminal 
5. Make LAMMPS by entering `emmake make emcc-serial mode=shlib` in terminal. Note that it is crucial that you use __Makefile.emcc-serial__ and that you use the __shlib__ flag to build LAMMPS. Without the flag, you cannot use LAMMPS on the browser. 
6. Verify that `liblammps.bc` and `liblammps_emcc_serial.bc` files are created

> LAMMPS was succesfully created. Note that in order to use the compiled LAMMPS in __another__ C++ project, you need to reference the entire `src` directory to include all the headers and build the other C++ project with the `liblammps.bc` and `liblammps_emcc_serial.bc` files! 


## Note from LAMMPS authors
### This is the LAMMPS software package.
LAMMPS stands for Large-scale Atomic/Molecular Massively Parallel
Simulator.

Copyright (2003) Sandia Corporation.  Under the terms of Contract
DE-AC04-94AL85000 with Sandia Corporation, the U.S. Government retains
certain rights in this software.  This software is distributed under
the GNU General Public License.

----------------------------------------------------------------------

LAMMPS is a classical molecular dynamics simulation code designed to
run efficiently on parallel computers.  It was developed at Sandia
National Laboratories, a US Department of Energy facility, with
funding from the DOE.  It is an open-source code, distributed freely
under the terms of the GNU Public License (GPL).

The primary author of the code is Steve Plimpton, who can be emailed
at sjplimp@sandia.gov.  The LAMMPS WWW Site at lammps.sandia.gov has
more information about the code and its uses.

The LAMMPS distribution includes the following files and directories:

README			   this file
LICENSE			   the GNU General Public License (GPL)
bench			   benchmark problems
couple			   code coupling examples using LAMMPS as a library
doc			   documentation
examples		   simple test problems
lib			   libraries LAMMPS can be linked with
potentials		   interatomic potential files
python			   Python wrapper on LAMMPS as a library
src			   source files
tools			   pre- and post-processing tools

Point your browser at any of these files to get started:

doc/Manual.html	           the LAMMPS manual
doc/Section_intro.html	   hi-level introduction to LAMMPS
doc/Section_start.html	   how to build and use LAMMPS
doc/Developer.pdf          LAMMPS developer guide
