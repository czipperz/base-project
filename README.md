# MYPROJECT

This repository provides a base project for C++ projects.

This repository is licensed under GPL3.  If you wish to
purchase a different license, email czipperz AT gmail DOT com.

Features:
* CMake build script.
* cz and Tracy integration.
* GNU Global tag generation.
* Build scripts (debug, release, release-debug, tracy).
* Catch2 tests.

Getting started:
1. Clone the repository by following step 1 of [Building](#Building).
2. Change all instances of `MYPROJECTURL` with the url of your project.
3. Change all instances of `MYPROJECT` with the name of your project.
4. Update `cz` submodule.
5. Delete this part of the readme.

The template project builds a program.  To make a library:
1. Change step 3 of the build instructions below.
2. Delete or rewrite the [Optimizing](#Optimizing) section.
3. Make the following changes to `CMakeLists.txt`:
   a. Remove all lines including `PROGRAM_NAME`.
   b. Change `LIBRARY_NAME` to `${PROJECT_NAME}` (no `-test` suffix).






## Building

1. Install the dependencies (see below).

2. Clone the repository and the submodules.

```
git clone MYPROJECTURL
cd MYPROJECT
git submodule init
git submodule update
```

3. Build MYPROJECT by running (on all platforms):

```
./build-release
```

4. After building, MYPROJECT can be ran via `./build/release/MYPROJECT`.

### Linux and OSX

Required packages: a C++ compiler, ncurses, and SDL (`SDL2`, `SDL2_image`, `SDL2_ttf`).

On Ubuntu you can install: `libncurses5 libsdl2-dev libsdl2-image-2.0-0 libsdl2-ttf-2.0-0`.

On Arch you can install: `ncurses sdl2 sdl2_image sdl2_ttf`.

### Windows

After cloning but before building you must download the [SDL], [SDL_ttf], and [SDL_image]
"Development Libraries" and place them in the `SDL`, `TTF`, and `IMG` directories, respectively.

[SDL]: https://www.libsdl.org/download-2.0.php
[SDL_ttf]: https://www.libsdl.org/projects/SDL_ttf/
[SDL_image]: https://www.libsdl.org/projects/SDL_image/

You will also need to install [ImageMagick] as it is used to generate MYPROJECT's icons.

[ImageMagick]: https://imagemagick.org/script/download.php

Next, to build the project you can either use the Visual Studio gui or the Windows build script.

* To use the Visual Studio gui, open the project as a
  folder in Visual Studio and click Build -> Build All.
* To use CMake, run the PowerShell build script: `.\build-release.ps1`.  But you must set
  `$env:VCINSTALLDIR` to the path of the `VC` directory (for example `$env:VCINSTALLDIR =
  "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC"`).

After building, MYPROJECT can be ran via `.\build\release\MYPROJECT.exe`.






## Optimizing

You can use Tracy to profile your project.  See [the Tracy manual] for more information.

[the Tracy manual]: https://bitbucket.com/wolfpld/tracy/downloads/tracy.pdf

First we have to build the Tracy configuration of MYPROJECT and build the Tracy
profiler.  Then run the profiler, and finally run the Tracy build of MYPROJECT.

Build MYPROJECT with Tracy enabled:
```
./build-tracy
```

Build `tracy/profiler` by following the instructions in the Tracy manual.  For example, on *nix:
```
cd tracy/profiler/build/unix
make release
```

Then we run Tracy:
```
./tracy/profiler/build/unix/Tracy-release &
```

Then run MYPROJECT with Tracy enabled.  Run it as the
super user to enable context switching recognition.
```
sudo ./build/tracy/MYPROJECT
```
