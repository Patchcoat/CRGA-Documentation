Getting Started
===============

.. _installation:

Installation
------------

Download the release for your operating system and unzip it: https://github.com/Patchcoat/CRGA/releases/tag/0.1
* Linking libraries in gcc: https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html
  * specify a location with ``-L/directory/path/`` and link the library with ``-llibcrga.so``
* Linking libraries with cmake: https://cmake.org/cmake/help/latest/command/target_link_libraries.html
  * specify a location with ``target_link_libraries(crga -L/directory/path/)``

.. _building:

Building
--------
It is possible to build the entire API locally

1. clone https://github.com/Patchcoat/CRGA.git onto your machine
2. run ``cmake .`` or the equivalent for your setup
3. build the project
  * On linux with gcc, cmake will generate a makefile. You can build the project by typing "make" into the terminal
  * On windows with the visual studio compiler, cmake will generate an sln and several vxcproj files. This can be built within visual studio, or by running ``msbuild crga.sln``
