# Rtools 4.0 ![status](https://img.shields.io/badge/status-highly_experimental-ff6600.svg)

*Last updated: March 30, 2018*

Testing R on Windows using an alpha version of gcc-8. If things go well, we may consider upgrading the official rtools toolchain for the next major release of R.

Currently the build of base R succeeds but fails checks. See log files:

 1. win32 build: [32bit.log](32bit.log): ![warnings](https://img.shields.io/badge/build-warnings-ff6600.svg)
 2. win64 build: [distribution.log](distribution.log): ![warnings](https://img.shields.io/badge/build-warnings-ff6600.svg)
 3. make check-all: [check.log](check.log): ![failed](https://img.shields.io/badge/build-failed-ff0000.svg)

