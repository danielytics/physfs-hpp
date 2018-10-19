PhysFS++ (the header only version)
========

PhysFS++ is a C++ header-only wrapper for the excellent [PhysicsFS library][1] by Ryan C.
Gordon and others.

This is a fork of the [original](https://github.com/kahowell/physfs-cpp) C++ wrapper. I found it a bit silly to have to carry around an extra .dll/.so file for such a small wrapper. 
This project just moved the implementation code around so that you don't need to build and link against phyfs++. Just configure your compiler to use PhysicsFS as you would do anyway and you don't have anything extra to do.

[1]: http://icculus.org/physfs

It is licensed under the zlib license - same as PhysicsFS (at the time of 
writing).

Usage
=====

Point your compiler's include path to (or add to your project)

In only **one** single .cpp file (one single compilation unit): define the implementation point of the library

```cpp
#define PHYFSPP_IMPL
#include "physfs.hpp"
```

Then, you can just include `physfs.hpp` and uses it's C++ interface instead of the plain old C one.

Requirements
============
The PhysicsFS library.

Features
========
The wrapper simply wraps most functions in a PhysFS namespace, and gives them 
C++ signatures (`std::string` rather than `const char *`).

Additionally:
 - Functions that are related to byte order conversions are placed in the 
PhysFS::Util namespace.
 - Instead of replicating `PHYSFS_openRead`, `PHYSFS_openWrite`, and 
`PHYSFS_openAppend`, files are opened as streams using `PhysFS::ifstream` and 
`PhysFS::ofstream`.
 - ofstream's constructor takes a mode, which specifies either append or write.
 - Both ifstream and ofstream are standard streams, and only have an extra
 method - `length`, which calls `PHYSFS_fileLength`.
