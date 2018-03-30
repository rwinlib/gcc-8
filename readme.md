## Rtools 4.0 ![status](https://img.shields.io/badge/status-highly_experimental-ff6600.svg)

*Last updated: March 30, 2018*

Testing R on Windows using an alpha version of gcc-8. If things go well, we may consider upgrading the official rtools toolchain for the next major release of R.

### Status

Currently the build of base R succeeds (with compiler warnings), but there are problems with C++ packages.

 1. [win32 build: ![warnings](https://img.shields.io/badge/build-warnings-ff9933.svg)](32bit.log)
 2. [win64 build: ![warnings](https://img.shields.io/badge/build-warnings-ff9933.svg)](distribution.log)
 3. [make check-all: ![warnings](https://img.shields.io/badge/build-warnings-ff9933.svg)](check.log)
 4. Rcpp: ![failed](https://img.shields.io/badge/build-failed-ff0000.svg)

