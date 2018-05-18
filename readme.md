# Rtools 4.0 

*Last updated by Jeroen, May 18, 2018*

![status](https://img.shields.io/badge/status-highly_experimental-ff6600.svg)

We are currently testing R on Windows using a test build of `gcc-8.1.0` with `mingw-w64 v5` runtime. If things go well, we may consider upgrading the official rtools toolchain for the next major release of R.

## Download

__This is an experimental toolchain for testing purposes only! It is not the official rtools!__ 

 - The `mingw32` toolchain: [i686-810-posix-dwarf-rt_v5-s](https://cloud.r-project.org/bin/windows/Rtools/i686-810-posix-dwarf-rt_v5-s.7z)
 - The `mingw64` toolchain: [x86_64-810-posix-seh-rt_v5-s](https://cloud.r-project.org/bin/windows/Rtools/x86_64-810-posix-seh-rt_v5-s.7z)

To test building R packages with this new toolchain, extract it to e.g. `C:/gcc-8.1.0/mingw32` and `C:/gcc-8.1.0/mingw64`. Then set the `BINPREF` variable in your `~/.Renviron` file (home is your Documents folder on Windows):

```sh
BINPREF="C:/gcc-8.1.0/mingw$(WIN)/bin/"
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
