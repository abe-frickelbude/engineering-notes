
# PlatformIO notes

## General

* All relevant project settings reside in `platformio.ini`

## Custom AVR packages / toolchains

* Can be found at <https://registry.platformio.org/tools/platformio/toolchain-atmelavr/versions>
  * The <https://registry.platformio.org> can generally be used to search for any package available via the PlantformIO trusted registry
* Can then be specified in `platformio.ini` in the `[env:]` section as e.g. 

```
platform_packages = platformio/toolchain-atmelavr@^3.70300.220127
```

## Passing compiler options to GCC

Add the following to the `[env:]` section in `platform.ini`:

```
build_flags = -Os 
```

The above example will enable "optimize for size" option.


## Generating "intermediate" assembler files 

Modify the above build flags (temporarily) as described below:

```
build_flags = -Og -fno-lto -fverbose-asm --save-temps
```

Here:

* `-Og` produces optimized code but also adds debugging information, may be useful for correlating to original C/C++ code
  * Generally speaking other optimization options also work fine, e.g. `-Os` for size
* `-fverbose-asm` increases verbosity in generated ASM listings, essentially decorating code sections with the
    original code fragments and corresponding line numbers in a source file for easier navigation (see GCC documentation for details)
* `--save-temps` tells the compiler to save the intermediate files (default is into the same directory as the source code!)
* `-f-no-lto` is absolutely **CRUCIAL!** It disables link-time optimization - while it is active, the produced
  assembly listing will be completely garbled and unreadable. 
  * It is likely that GCC actually works as expected here,  but unfortunately totally undocumented in the usual tutorials / 
    HOWTOs on the interwebs. 
  * Original credit goes to an obsure thread here: <https://community.platformio.org/t/save-assembler-files-during-building/23085/3> 
  * Kudoz to the user for finding out that the `-flto` compiler switch is responsible for garbling the output