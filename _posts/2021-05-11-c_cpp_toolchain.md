---
layout: post
title: "C/C++ Toolchains"
date: Mon  7 Jun 08:23:36 +07 2021
categories: C C++
---

This note is about C/C++ toolchains in Linux systems.

# Terms

Talking about bulding of C/C++ toolchains, some terms will apply:

- BUILD system: The system which will do the compilation and run other programs for the building process (i.e. patch, sed).
- HOST system: The system which will run the resulted toolchain. Usually, BUILD system and HOST system are the same; but sometimes it's necessary to have different BUILD and HOST system. E.g. BUILD system is much stronger, or HOST system does have all necessary tools and libraries for the build.
- TARGET system: The system which will run binaries which will be created by the resulted toolchain.

# General Remarks

For all the use-cases, considering the following remarks may help to avoid troublesome situations:

- Compiling the whole toolchain could be exceedingly long. According to Linux From Scratch book, the first package of the toolchain is `binutils`, and its build time is considered as unit for other packages (1 SBU). Not counting other packages, a build pass of GCC usually takes 11 SBU, and GCC will be built by several passes! The final build pass (with tests) may takes 95 SBU. Depend on the use cases, the time needed could be **extremely long**. Normally, a toolchain generator like Crosstool-NG does not take that extreme and the build time is usually from 15 minutes to 60 minutes.
- Different versions of GCC apply different default code standards and configurations. What does this mean? A new version of GCC may refuse to compile a toolchain for older versions of GCC and related packages! People on the Internet cannot test all scenarios, so prepare yourselves for some debugging; especially when compiling toolchain with a build system of different era. Debugging usually results a rebuild, so prepare time too!
- A cross-toolchain is built for specified HOST system. If the toolchain is redistributed to another system, that system must be similar to the specified HOST. In concrete, binaries are usually compiled and linked with libc (i.e. glibc) and gcc/g++ libraries (i.e. libstdc++); those binaries may **fail** to run on systems with **older** libraries.

# Some Use-cases

## Compiling gcc for current system

This is the simplest use-case when we only need different version of gcc for any reasons.
However, the compilation may not be straight forward at all. Depending on your build system, various patches and hacks may be required. The best bet is using sources and build scripts from the BUILD distro, so that most, if not all, patches and hacks are already included.
The general rule of thumb still apply: It's more pain to compile a gcc of different era from BUILD system's.

## Compiling a toolchain for a similar system with the same architecture but different library verions

For example, both developer machine and deployment machine are of amd64 architecture, but the deployment machine has older glibc version. A symtom indicating that this use-case is necessary: a `helloworld` program built by developer machine and complains something like (just for demonstration):
```
undefined reference to symbol 'socket@@GLIBC_2.4'
```
And version of glibc in deployment machine is older than 2.4. NOTE: Double check that nothing is wrong with the linking in developer machine and deployment of libraries before conclude that a new toolchain is required.

Building a new toolchain involves installing kernel headers, compilation of `binutils`, `glibc` (or other libc) and `gcc` (several times!). This process is error-prone! There are guides on the Internet for build steps; e.g. linuxfromscratch is a good source. Be aware, as mentioned before, depending on the use-case and differences in versions, additional work (i.e. applying patches or manually change build flags) may be necessary, and must be carried out with certain understanding.
Using a toolchain generator like Crosstool-NG saves a lot of work, but doesn't guarantee a success.

Those are the warnings, but unless the use-case is too tricky, there is a good chance that the build is success. If you are stuck, stop and think thoroughly about your use-case and possibilities; DON'T aimlessly google and copy any hacks you found.

## Compiling a toolchain for a different architecture (cross-toolchain)

TODO

# References

- [Linux From Scratch](https://www.linuxfromscratch.org/lfs/view/stable/index.html)
- [Anatomy of Cross Compilation Toolchains](https://elinux.org/images/1/15/Anatomy_of_Cross-Compilation_Toolchains.pdf)
- [Crosstool-NG Documentation](https://crosstool-ng.github.io/docs/)

