# Rtools 4.0 

*Last updated by Jeroen, April 3, 2018*

![status](https://img.shields.io/badge/status-highly_experimental-ff6600.svg)

We are currently testing R on Windows using an alpha version of gcc-8. If things go well, we may consider upgrading the official rtools toolchain for the next major release of R.

## Download

__This is an experimental version for testing purposes only! It is not the official rtools!__ 
The alpha bundle contains:

 - Toolchains based on `gcc-8.0.1 (20180331)` with `mingw-w64 v5` runtime
 - Build utilities from `msys2` (march 2018)
 - ICU 58.2
 - Texinfo 5 (unchanged from rtools 3.4)

Download from CRAN: https://cloud.r-project.org/bin/windows/Rtools/rtools40_alpha.zip

To test R packages with the new toolchain, extract the bundle to e.g. `C:\rtools40` and put the following in your `~/.Renviron` file (home is your Documents folder on Windows):

```sh
PATH="C:\rtools40\bin;${PATH}"
BINPREF="C:/rtools40/mingw$(WIN)/bin/"
```

## Status

Currently the build of base R passes checks (with compiler warnings), and Rcpp now works as well.

 1. [win32 build: ![win32-build](https://img.shields.io/badge/build-warnings-EDB512.svg)](32bit.log)
 2. [win64 build + manuals: ![win64-build](https://img.shields.io/badge/build-warnings-EDB512.svg)](distribution.log)
 3. [make check-all: ![make-check](https://img.shields.io/badge/check-success-00dd00.svg)](check.log)
 4. [Rcpp: ![rcpp-check](https://img.shields.io/badge/check-success-00dd00.svg)](rcpp.log)

## External Libs

At least all C++ libraries that use `std::string` need a rebuild because the ABI has changed. Most other libraries that were built for gcc 4.9.3 may still work with gcc 8. Some early results:

 - Plain C libs: all OK
 - [V8](https://github.com/rwinlib/v8): OK
 - [tesseract](https://github.com/rwinlib/tesseract): OK
 - [gdal2](https://github.com/rwinlib/gdal2): Works for sf, need more testing
 - [protobuf](https://github.com/rwinlib/protobuf): definitely broken
 - [imagemagick6](https://github.com/rwinlib/imagemagick6): definitely broken
 - [poppler-cpp](https://github.com/rwinlib/poppler): definitely broken

## Known Issues

 - Building GDB doesn't work yet. Hopefully fixed when GCC 8.1 is released
 - Possible changes in `make`, `sh` and `tar` behavior due to undocumented patches in old rtools, see [README.txt](https://cloud.r-project.org/bin/windows/Rtools/README.txt)
 - Consider shipping rtools as a package manger rather than a fat bundle. That way we can push small updates and ship external libraries.
 - ...
