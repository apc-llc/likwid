

# Introduction #

Likwid is build using GNU make and has no external dependencies apart from
the Linux kernel and the standard  C library.

It should build on any Linux distribution with a recent gcc compiler
and 2.6 or newer kernel without any changes.

There is one generic top level Makefile and one .mk configuration file for each
compiler (at the moment gcc and icc). Please note that I can only test LIKWID
with gcc. icc is only tested for basic functionality.

There is one exception: If you want to use LIKWID on a Intel Xeon Phi card you have
to choose the MIC as Compiler in config.mk, which is based on Intel icc compiler.


# Directory structure #

All source files are in the _src_ directory. All header files are located in
_src/includes_ . Each application main source files are in
_src/applications_.

All build products are generated in the directory _./TAG_, where _TAG_ is the
compiler configuration, default _./GCC_.

# Configuration #

Usually the only thing you have to configure is the _PREFIX_  install path.

## Changing color of likwid-pin output ##

Depending on the background of your terminal window you can choose a color
for likwid-pin output.

## Usage of accessDaemon ##

Usually you can use LIKWID in the standard setup with direct access to the MSR
files. If you install LIKWID on a shared system as a HPC compute cluster you
may consider to use the accessDaemon. This is a proxy application which was
implemented with security in mind and performs address checks for allowed access.
Using the accessDaemon the measurements involve more overhead, especially if you use
likwid-perfctr in timeline mode or with the marker API.

To enable using the accessDaemon:

  1. Set BUILDDAEMON to true
  1. Configure the path to the accessDaemon binary (usually keep default)
  1. Set the default ACCESSMODE

ACCESSMODE can be direct, accessdaemon and sysdaemon (not yet officially supported).
You can overwrite the default setting on the command line.

## Enable SandyBridge Uncore ##

This is only relevant if you also want to use LIKWID no SandyBridge. This
setting does not influence the usage of the same binary on other
microarchitectures. If you want to measure the Uncore counters on SandyBridge
you have to use the accesDaemon at the moment. If you need direct access you
can disable Uncore support for SandyBridge.

## Build likwid marker API as shared library ##

Per default the LIKWID library is build as a shared library. You need the library
is necessary if you want to use the Marker API. You can also use the LIKWID modules
directly. This is still not officially supported at the moment. In some settings it
is necessary to build LIKWID as a shared library. To do so set SHARED\_LIBRARY to true.

## Instrument likwid-bench for usage with likwid-perfctr ##

likwid-bench is instrumented for use with likwid-perfctr. This allows you to
measure various metrics of your likwid-bench kernels. Enable instrumentation by
setting INSTRUMENT\_BENCH to true.

## Enabling Fortran interface for marker API ##

If you want to use the Marker API in Fortran programs LIKWID offers a native
Fortran90 interface. To enable it uncomment he FORTRAN\_INTERFACE line.
More information using LIKWID with other programming languages is
in OtherLanguages.

# Build targets #

You have to edit config.mk to configure your build and install path.

The following make targets are available:

  * **make** - Build all applications apart from likwid-bench
  * **make likwid-bench** - Build likwid-bench
  * **make clean** Remove the object file directory _./GCC_, keep the executables
  * **make distclean** Remove all generated files

The build system has a working dependency tracking, therefore make clean is only
needed if you change the Makefile configuration.

# Installing #

NOTE: The pinning functionality and the !accessDaemon only works if configured in config.mk and
installed with **make install**. If you do not use the pinning functionality the tools
can be used without installation.

  * **make install** - Installs the executables, libraries, man pages and headers to the path you configured in config.mk.
  * **make uninstall** - Delete all installed files.

# Setting up access for hardware performance monitoring #

Hardware performance monitoring on x86 is configured using model-specific
registers (MSR). MSR registers are special registers not part of the
instruction set architecture. To read and write to these registers the x86 ISA
provides special instructions. These instructions can only be executed in
protected mode or in other work only kernel code can execute these
instructions. Fortunately any Linux kernel 2.6 or newer provides access to these
registers via a set of device files. This allows to implement all of the
functionality in user space. Still it does not allow to use those more advanced
features of hardware performance monitoring which require to setup
interrupt service routines.

Per default only root has read/write access to these msr device files. In order
to use the LIKWID tools, which need access to these files (likwid-perfctr and
likwid-powermeter) as standard user you need to setup access rights to these
files.

likwid-perfctr, likwid-powermeter and likwid-features require the Linux msr
kernel module. This module is part of most standard distro kernels. You have to
be root to do the initial setup.

1. Check if the msr module is loaded with  _lsmod | grep msr_ . There should be an output.
2. It the module is not loaded load it with  _modprobe msr_ . For automatic loading at startup
consult your distros documentation how to do so.
3. Adopt access rights on the msr device files for normal user. To allow everybody access you can
use **chmod o+rw /dev/cpu/_/msr_ . This is only recommended on single user desktop systems.**

As a general access to the msr registers is not desired on security sensitive
systems you can either implement a more sophisticated access rights settings
with e.g. setgid. A common solution used on many other device files, e.g. for
audio, is to introduce a group and make a chown on the msr device files to that
group. Now if you execute likwid-perfctr with setgid on that group the
executing user can use the tool but cannot directly write or read the msr
device files.

Some distributions backported the capabilities check for the msr device to older kernels. If there are problems with accessing the msr device for older kernels with file system permissions set to read&write, please check your kernel code (_arch/x86/kernel/msr.c_) for the backport and set the MSR capabilities in case.

A secure solution is to use the [accessDaemon](MSRDaemon.md), which encapsulates
the access to the msr device files and performs a address check for allowed
registers. For more information how to setup and use this solution have a look
at the [WIKI page](MSRDaemon.md).

If you have problems please let me know on the
[likwid user mailing list](http://groups.google.com/group/likwid-users)


## Setting up access to SandyBridge Uncore ##

Starting with SandyBridge Intel started to use PCI config address memory to
configure and use the Uncore hardware performance monitoring. In Linux there is
no way to gain access to this mapped address ranges as normal user. Therefore
likwid-perfctr can only be used with the SandyBridge Uncore if using the
accessDaemon setup with setuid root. Note that you can overwrite this on the
command line if you , e.g., want to make very accurate measurements as root in
DIRECT mode.
A demo for a root exploit involving the msr device files was published. As a consequence the security settings for access to the msr device files are tightened in recent kernels.

## Issues on recent kernels ##

Just setting the file access rights or using suid root on the access daemon is not sufficient anymore. You have to register your binary now to get access.

This is done by calling

`sudo setcap cap_sys_rawio+ep EXECUTABLE`

on the executables. This is only possible on local file systems. A feasible way is to use the likwid-accessD for all accesses and just enable the capabilities for this one binary. This will enable the usage for all LIKWID tools and also for all instrumented binaries. If the likwid-perfctr utility should only be used in wrapper mode, it is suitable to set the capabilities for likwid-perfctr only. Please remember to set the file permission of the MSR device file to read/write for all users, even if capabilites are configured correctly.


