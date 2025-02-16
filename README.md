This is a fully functional freecloth port by Dr. Muhammad Mobeen Movania which has been tested on Windows 10 x64 machine on MS Visual Studio 2019. This port includes all dependencies so you should be able to compile and run the application without any issues. Just open the freeglut.sln Visual Studio project and then run the clothApp. There were some issues in the code esp glutInit call was not made which was failing the glut initialization. All errors have been fixed so if everything goes well, you should see this window.
![image](https://github.com/user-attachments/assets/1e4b9162-6d13-4cf0-b4ea-161067de8914)

/////////////////////////////////
// Original readme starts here //
/////////////////////////////////

Freecloth
http://freecloth.enigmati.ca

(c) 2002-2003 David Pritchard

License: GNU LGPL v2


SUMMARY
=======


Freecloth is a free, open-source cloth simulation tool. It is intended to help
with further research in cloth simulation, and to help in production of feature
films or games using cloth. In its initial form, the simulation has been
implemented using algorithms described in Baraff & Witkin's "Large Steps
in Cloth Simulation" paper. As development advances, it should hopefully
incorporate newer techniques for collision detection and other features. It
will hopefully match or exceed the capabilities of commercial cloth simulations
like Alias | Wavefront's "Maya Cloth" or Kelseus Cloth for 3dsmax.

Freecloth is not yet ready for regular users. It's still under development,
and does not have a polished user interface, or plugins for popular modeling
software packages. At present, there's just a library and a small demonstration
application.

This cloth simulator uses techniques that are more advanced than most
comparable free packages. Most simple simulators use explicit integration,
which is easy to implement and fairly fast for small pieces of cloth. Freecloth
uses implicit integration, which is harder to implement but gives much better
results for large pieces of cloth. For explicit techniques to work with large
pieces of cloth, stretch forces have to be greatly reduced, and the cloth will
look "rubbery," bouncing and stretching in unrealistic ways. The implicit
technique used by Freecloth allows detailed animation of cloth without
excessive stretch.

Freecloth is written in C++. The library has no external dependencies, but
the demonstration application requires OpenGL, GLUT and GLUI. It has been
compiled on Linux (gcc 2.95, gcc 3.2 and gcc 3.3) and under Windows (Visual
C++ 6.0), and it should be straightforward to port to other operating systems,
provided that a reasonably conformant C++ compiler is available. Solid C++
engineering techniques have been applied to create a fairly robust and modern
application.

This project began as a course project. An updated version of the report
produced for that project is available from the Freecloth website [1].
Source code and some binaries are available from the Sourceforge site [2].
    [1] http://freecloth.enigmati.ca/docs/report-chaps/
    [2] http://sourceforge.net/project/showfiles.php?group_id=54926


TABLE OF CONTENTS
=================

1. Installation
    1.1. Basic installation
2. Usage
    2.1. Library
    2.2. Test application
3. Algorithms
4. Bugs
    4.1. Library
    4.2. Test application




1. Installation
---------------

No additional libraries are needed to compile the Freecloth library.
These libraries are needed to compile the Freecloth test application:

    OpenGL and GLU
    GLUT
        http://www.xmission.com/~nate/glut.html
    GLUI 2.1
        http://www.cs.unc.edu/~rademach/glui/


1.1. Linux
----------

cd freecloth-0.x.y
./configure
make install

Tips:
- if you have headers or libraries in nonstandard directories, try defining a
  few environment variables, e.g.,
    export CPPFLAGS=-I$HOME/include
    export LDFLAGS=-L$HOME/lib
  When you run the configure script, it will then try to use these flags when
  calling the C/C++ compiler and linker.


1.2. Windows (Visual C++)
-------------------------

Open freecloth-0.x.y/freecloth/freecloth.dsw.
Select Debug or Release build.
Change any necessary settings (include paths, library paths).
Compile.

Open freecloth-0.x.y/freecloth/clothApp.dsw.
Select Debug or Release build.
Change any necessary settings (include paths, library paths).
Compile.


2. Usage
--------

2.1. Library
------------

Instructions for linking, including, etc. to come later...

The full API reference is available at
    http://freecloth.enigmati.ca/docs/public/html/


2.2. Test application
---------------------

Linux: run freecloth/clothApp/clothApp
Windows: run freecloth/Release/clothApp.exe

The user interface is fairly straightforward. The important buttons are the
"run", "step", "stop" and "rewind" buttons, which execute the program.

A few important notes:

- when adaptive timestepping is used (the default), each step corresponds to
  a single animation frame, which is by default 0.04 seconds. This may seem a
  little slow.
- large cloth sizes run very slowly. For a 200x200 cloth, 20 to 30 seconds per
  step is not uncommon.
- if the simulation stops and can't advance, there's probably an instability
  in the simulation due to excessive stretch. Rewind, and try again with one
  of the following:
    - adaptive timestepping and a lower stretch limit
    - basic timestepping and a small timestep
    - higher stretch constant


3. Algorithms
-------------

Freecloth is based upon the algorithm described in "Large Steps in Cloth
Simulation" by David Baraff and Andrew Witkin. It is almost a complete
implementation of this paper. At present, the only part of the paper that has
not been implemented is collision detection. Corrections from Uri Ascher and
Eddy Boxerman's "On the modified conjugate gradient method in cloth simulation"
have also been incorporated.

In the future, it would be useful to incorporate some of the simulation ideas
from Choi and Ko's 2002 SIGGRAPH paper, Bridson et. al's collision
detection and friction algorithm from SIGGRAPH, and Bridson et. al's upcoming
cloth simulation paper at the 2003 Symposium for Computer Animation.


4. Bugs
-------

4.1. Library
------------

- No known major bugs.


4.2. Test Application
---------------------

- GLUI has plenty of bugs in the text input controls.
- GLUI seems to have a lot of refreshing problems under Windows.
- Snapshots are a little hackish, and prone to failure.
- There may still be some bugs when changing parameters while the program runs.
