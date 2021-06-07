---
layout: post
title: "C/C++ Toolchains"
date: Mon  7 Jun 08:23:36 +07 2021
categories: C C++
---

This note is about C/C++ toolchains in Linux systems.

# General Remarks

For all the use-cases, considering the following remarks may help avoiding troulesome situations:

- Compiling the whole toolchain could be exceedingly long. According to Linux From Scratch book, the first package of the toolchain is `binutils`, and its build time is considered as unit for other packages (1 SBU). Not counting other packages, a build pass of GCC usually takes 11 SBU, and GCC will be built by several passes! The final build pass (with tests) may takes 95 SBU. Depend on the use cases, the time needed could be **extremely long**. Normally, a toolchain generator like Crosstool-NG does not take that extreme and the build time is usually from 15 minutes to 60 minutes.
- Different versions of GCC apply different default code standards and configurations. What does this mean? A new version of GCC may refuse to compile a toolchain for older versions of GCC and related packages! People on the Internet cannot test all scenarios, so prepare yourselves for some debugging; especially when compiling toolchain with a build system of different era. Debugging usually results a rebuild, so prepare time too!

# Some Use-cases

## Compiling gcc for current system

This is the simplest use-case when we only need different version of gcc for any reasons.

## Compiling a toolchain for a similar system with the same architecture but different library verions

TODO

## Compiling a toolchain for a different architecture (cross-toolchain)

TODO

# References

- [Linux From Scratch](https://www.linuxfromscratch.org/lfs/view/stable/index.html)
- [Anatomy of Cross Compilation Toolchains](https://elinux.org/images/1/15/Anatomy_of_Cross-Compilation_Toolchains.pdf)
- [Crosstool-NG Documentation](https://crosstool-ng.github.io/docs/)