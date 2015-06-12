# Release 3.1.3 #

  * Full Uncore Support for Nehalem EX and Westmere EX
  * Atom Silvermont (Avoton + BayTrail) support
  * Read Marker API results and derived metrics in instrumented application (Patch by Julian Kunkel)
  * More low-level benchmarks for likwid-bench
  * Kernel module for enabling the RDPMC instruction
  * Use RDPMC for fixed and general purpose core-local counters if possible
  * New undocumented but working events
  * Support for all RAPL domains in likwid-powermeter
  * Better PCI device lookup
  * Lots of bug fixes

# Release 3.1.2 #
  * New application likwid-setFrequencies and corresponding daemon likwid-setFreq
  * likwid-powermeter can measure multiple sockets at once
  * likwid-memsweeper also  cleans last level cache from dirty cachelines
  * Sanitized groups for Intel IvyBridge and SandyBridge
  * Automatic lookup of Uncore PCI devices with exclusion of non-existent devices
  * Reduced connect time to likwid-accessD
  * Multiple workgroups for likwid-bench are evaluated correctly
  * MSR device file handling on Intel Xeon Phi improved
  * Improved commandline argument handling for all LIKWID tools
  * man pages sanitized and a new one for likwid-bench
  * Moved setuid command to sbin directory
  * Lots of bugfixes

# Release 3.1 #

  * Full support for Intel Xeon Phi
  * Support for Intel IvyBridge-EP (partial Uncore support)
  * Support for Intel Haswell
  * Support for AMD Kabini architecture
  * Improved Intel Atom support
  * Adding expression based thread group syntax for all LIKWID tools
  * Add scatter option to thread groups
  * Add possibility to dump topology info to cfg file. This enables simpler usage of LIKWID in a restricted cpuset
  * Using the Marker API a variable number of threads may enter a region now
  * Simple lock file based control to synchronize Monitoring and Profiling in a cluster environment
  * Using custom event sets on Intel Processors fixed counters are automatically added and connected derived metrics runtime, clock and CPI are output
  * Oversubscription of processors with round  robin placement is now default
  * Add event for TM/TM2 temperature sensors on Intel processors
  * Improved RDTSC timing measurement
  * Review of performance groups
  * Performance improvements in Marker API
  * Lots of bugfixes and improvements

# Release 3.0 #

  * New application likwid-memsweeper to cleanup ccNUMA memory domains. This functionality is also integrated in likwid-pin.
  * Support for Intel SandyBridge Uncore (partial)
  * Support for Intel IvyBridge (only core part)
  * Initial support for Intel Xeon Phi (KNC)
  * Better support for AMD Interlagos
  * The OpenMP type is now detected automatically while pinning
  * Lots of bugfixes and improvements
  * Marker API works now for threaded code and accessDaemon
  * Uncore support for timeline mode
  * Convenient macro wrapper for Marker API
  * Data volume as new metric in all memory/cache groups
  * Updated Wiki documentation

# Release 2.3 #

  * New application likwid-powermeter to measure Energy consumption on SandyBridge (RAPL) and query turbo mode steps.
  * RAPL counters are also integrated into likwid-perfctr
  * likwid-mpirun: Many improvements and initial support for mvapich2
  * likwid-mpirun has now integrated perfctr support
  * Much improved fortran interface for the marker API
  * Support for Intel SandyBridge
  * Support for AMD Interlagos
  * Initial support for NehalemEX and WestmereEX Uncore
  * Better default options for likwid-pin
  * Lots of Bugfixes and small improvements

# Release 2.2 #

  * New application likwid-perfscope as frontend to timeline mode of likwid-perfctr
  * Initial support for OpenMPI in likwid-mpirun
  * Initial support for Intel SandyBridge (Core) in likwid-perfctr
  * Improvements in likwid-msrD
  * Native Fortran 90 interface for Marker API
  * Completetly rewrite of marker API. Simplified usage. Allows now inclusive and overlapping regions.
  * New output filter subsystem. Allows you to define your own output file formats and filters. Default comes with CSV and XML formats.

# Release 2.1 #

  * likwid-perfctr supports output in files with placeholders for MPI settings
  * improved and extended performance groups in likwid-perfctr
  * msr daemon added for encapsulation of msr device file access (experimental)
  * add numa thread domains (M prefix) in affinity module
  * fix bug in likwid-bench code generation preventing correct loop generation
  * better dependency tracking in build system
  * Extended documentation
  * likwid-perfctr also includes now the pin functionality
  * Again switch back to cpumask sys interface for the cpu to node mapping
  * likwid-mpirun script enables simple pinning of pure MPI or hybrid OpenMP/MPI

# Release 2.0 #

  * likwid-pin and likwid-perfctr supports logical pinning (node, socket, cache group)
  * likwid-perfctr supports multiple instance marker API runs on the same node
  * performance groups in likwid-perfctr are now generated from simple text files
  * likwid-topology also reports on NUMA information
  * Support for second fixed counter on Intel CPUS
  * likwid-pin can set NUMA mempolicy
  * statistical output in likwid-perfctr for threaded results
  * support for Nehalem EX core events in likwid-perfctr
  * likwid-perfctr allows lightweight continous measurements with daemon mode
  * silent mode switch for likwid-pin