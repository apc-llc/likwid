﻿#summary likwid-perfctr User Manual version 3.1




# Introduction #

While there are already a bunch of tools around to measure hardware performance
counters a simple lightweight command line tool for simple end to end
measurements was still missing. The Linux msr module providing an interface to
access model specific registers from user space allows us to provide a tool to
read out hardware performance counters with an unmodified linux kernel.

likwid-perfctr supports the following modes:

  * **wrapper mode**: Use likwid-perfctr as a wrapper to your application. You can measure without altering your code.
  * **stethoscope mode**: Measure performance counters for a variable time duration independent of any code running.
  * **timeline mode**: Output performance metric in specified frequency (can be ms or s)
  * **marker API**: Only measure regions in your code, still likwid-perfctr controls what to measure.

There are pre-configured event sets, called performance groups, with
useful pre-selected event sets and derived metrics. Alternatively you can specify a custom
event set. You can measure as many events in one run as there are physical
counters on a given CPU. See in the architecture specific pages for more
details. likwid-perfctr will validate during runtime if an event can be measured
on a configured counter.

Because likwid-perfctr performs simple end-to-end measurements and does not
know anything about the code which gets executed it is crucial to pin your
application. The relation between the measurement and your code is solely
through pinning. likwid-perfctr has all pinning functionality of likwid-pin
builtin. You need no additional tool for the pinning. Still you can control
affinity yourself if you prefer.

likwid-perfctr counter groups are simple text files and can be easily changed
or extended. It is simple to create your own performance groups with custom
derived metrics.

# Supported architectures #

For architecture specific information for likwid-perfctr click on the
architecture links below.

Intel:

  * [P6](P6.md) processors : Pentium 2, Pentium 3 (deprecated)
  * [PentiumM](PentiumM.md) : Banias, Dothan (deprecated)
  * [Core2](Core2.md) : 65nm Dual Core, 45nm Dual and Quad Core
  * [Nehalem](Nehalem.md) : all variants
  * [NehalemEX](NehalemEX.md) : only partial support for Uncore
  * [Westmere](Westmere.md) : all variants
  * [WestmereEX](WestmereEX.md) : only partial support for Uncore
  * [SandyBridge](SandyBridge.md) : Desktop and EP server variants. Support for energy counters. Partial support for Uncore.
  * [IvyBridge](IvyBridge.md) : Desktop  and EP server variants. Support for energy counters. Partial support for Uncore.
  * [Haswell](Haswell.md) :  Desktop
  * [KNC](KNC.md) : Intel Xeon Phi KNC

AMD:

  * [K8](K8.md) : all variants
  * [K10](K10.md) : Barcelona, Shanghai, Istanbul and MagnyCours
  * [Interlagos](Interlagos.md) : Full support including Uncore
  * [Kabini](Kabini.md) : Full support including Uncore

# Prerequisites #

The following prerequisites must be met:

  * The msr module must be loaded (or compiled into the kernel) and the user must have read/write access to the /dev/cpu/`*`/msr files
  * For newer Intel processor Uncore support you must use the provided likwid-accessD  with setuid root setup.
  * For recent kernels in addition you have to set the capability for likwid-accessD to allow to access the msr device files.

If the MSR module is not compiled into the kernel right away, you have to load it manually. Execute as root:
```
modprobe msr
```

If you want to use likwid-perfctr from user space you have to set according
rights on the device files on the /dev/cpu/[0-9]/msr files. You can also
introduce a special group which is allowed to read and write to the device
files.

To set the basic rights for everyone as root execute:

```
chmod o+rw /dev/cpu/*/msr
```

See also the file INSTALL for further details. In security sensitive areas, as
on multi user systems or HPC clusters the uncontrolled access to all MSR
registers is a security problem. For solutions to this issue have a look at
[Build](Build.md) and [MSRDaemon](MSRDaemon.md).

# Options #

```
-h Help message
-v Version information
-V verbose output
-g performance group  or event set string
-H Get group help (together with -g switch)
-t timeline mode with frequency in s or ms, e.g. 300ms
-S stethoscope mode with duration in s
-m use markers inside code
-s bitmask with threads to skip
-o Store output to file, with output conversation according to file suffix
   Conversation scripts can be supplied in /usr/local/share/likwid
-O Output easily parseable CSV instead of fancy tables
-M set how MSR registers are accessed: 0=direct, 1=msrd
-a list available performance groups
-e list available counters and events
-i print cpu info
-c processor ids to measure (required), e.g. 1,2-4,8
-C processor ids to measure (this variant also cares for pinning of process/threads), e.g. 1,2-4,8
```

# Basic Usage (Wrapper mode) #

Output help text  with
```
likwid-perfctr -h
```

There are two required flags: -c to configure for which core ids the counters
should be measured and -g to specify which group or event set you want to measure. The core id list is a comma separated list which can also contain
ranges. This list can be specified in all variants supported by LikwidPin, from
physical processor ids to different logical variants. To figure out the thread
and cache topology you can use likwid-topology. As likwid-perfctr measures
processors and has no knowledge about your process or threads, you have to
ensure that your code you want to measure really runs on the processors you
sense with likwid-perfctr. likwid-perfctr includes all functionality of
likwid-pin for pinning a threaded application. Alternatively you can also care
yourself for the pinning with another tool or from within the code.

For gathering information about hardware performance capabilities and
performance groups use the `-a`, `-g` and `-H` switches.

```
likwid-perfctr -a
```
prints all supported groups on a processor to stdout.

To get a list with all supported counter registers and events call
```
likwid-perfctr -e | less
```

A help text explaining a specific event group can be requested with `-H`
together with the `-g` switch:
```
likwid-perfctr -H -g MEM
```

To use ikwid-perfctr for a serial application execute, e.g.:
```
likwid-perfctr  -C S1:0  -g FLOPS_DP  ./a.out
```

This will pin the application to the first core on socket one and
measure the performance group FLOPS\_DP on this core.
The output for the serial application could look like as follows:
```
-------------------------------------------------------------
CPU type:       Intel Core Lynnfield processor 
CPU clock:      2.93 GHz 
-------------------------------------------------------------
Measuring group FLOPS_DP
-------------------------------------------------------------
YOUR PROGRAM OUTPUT
+--------------------------------------+-------------+
|                Event                 |   core 0    |
+--------------------------------------+-------------+
|          INSTR_RETIRED_ANY           | 7.29301e+08 |
|        CPU_CLK_UNHALTED_CORE         | 1.3482e+09  |
|    FP_COMP_OPS_EXE_SSE_FP_PACKED     | 1.32108e+08 |
|    FP_COMP_OPS_EXE_SSE_FP_SCALAR     |     724     |
| FP_COMP_OPS_EXE_SSE_SINGLE_PRECISION |      0      |
| FP_COMP_OPS_EXE_SSE_DOUBLE_PRECISION | 1.32108e+08 |
+--------------------------------------+-------------+
+--------------------------+------------+
|          Metric          |   core 0   |
+--------------------------+------------+
|       Runtime [s]        |  0.459607  |
|           CPI            |  1.84861   |
| DP MFlops/s (DP assumed) |  574.874   |
|      Packed MUOPS/s      |  287.436   |
|      Scalar MUOPS/s      | 0.00157526 |
|        SP MUOPS/s        |     0      |
|        DP MUOPS/s        |  287.438   |
+--------------------------+------------+
```

The output will always consist of a table with the raw event counts and another
table with derived metrics. The columns are the processor ids measured.
If you measure more than one core there is another table with statistical
data as min, max and mean.

The events have the same naming as in the official processor manuals. The
relevant manuals are the Intel Software Development Manual 3B Appendix A and
for AMD the BIOS and Kernel Developers Guides (BKDG) of the appropriate processor.
You can also have a look in the Optimization manuals provided by the vendors
for interesting event sets.

# Basic threaded usage #

For threaded use nothing changes apart from the -C command line arguments.
Example for a threaded STREAM benchmark compiled with OpenMP (note that if you omit `OMP_NUM_THREADS` it will be set by likwid):

```
likwid-perfctr  -C 0-3 -g FLOPS_DP  ./stream-icc

-------------------------------------------------------------
CPU type:       Intel Core Lynnfield processor 
CPU clock:      2.93 GHz 
-------------------------------------------------------------
Measuring group FLOPS_DP
-------------------------------------------------------------
YOUR PROGRAM OUTPUT
+--------------------------------------+-------------+-------------+-------------+-------------+
|                Event                 |   core 0    |   core 1    |   core 2    |   core 3    |
+--------------------------------------+-------------+-------------+-------------+-------------+
|          INSTR_RETIRED_ANY           | 1.97463e+08 | 2.31001e+08 | 2.30963e+08 | 2.31885e+08 |
|        CPU_CLK_UNHALTED_CORE         | 9.56999e+08 | 9.58401e+08 | 9.58637e+08 | 9.57338e+08 |
|    FP_COMP_OPS_EXE_SSE_FP_PACKED     | 4.00294e+07 | 3.08927e+07 | 3.08866e+07 | 3.08904e+07 |
|    FP_COMP_OPS_EXE_SSE_FP_SCALAR     |     882     |      0      |      0      |      0      |
| FP_COMP_OPS_EXE_SSE_SINGLE_PRECISION |      0      |      0      |      0      |      0      |
| FP_COMP_OPS_EXE_SSE_DOUBLE_PRECISION | 4.00303e+07 | 3.08927e+07 | 3.08866e+07 | 3.08904e+07 |
+--------------------------------------+-------------+-------------+-------------+-------------+
+--------------------------+------------+---------+----------+----------+
|          Metric          |   core 0   | core 1  |  core 2  |  core 3  |
+--------------------------+------------+---------+----------+----------+
|       Runtime [s]        |  0.326242  | 0.32672 | 0.326801 | 0.326358 |
|           CPI            |  4.84647   | 4.14891 | 4.15061  | 4.12849  |
| DP MFlops/s (DP assumed) |  245.399   | 189.108 | 189.024  | 189.304  |
|      Packed MUOPS/s      |  122.698   | 94.554  | 94.5121  | 94.6519  |
|      Scalar MUOPS/s      | 0.00270351 |    0    |    0     |    0     |
|        SP MUOPS/s        |     0      |    0    |    0     |    0     |
|        DP MUOPS/s        |  122.701   | 94.554  | 94.5121  | 94.6519  |
+--------------------------+------------+---------+----------+----------+
```

Please note that in previous version of LIKWID you had to specify the OpenMP
implementation used. This is not necessary anymore. LIKWID will figure out the
relevant properties of the code itself. On newer processors there is one issue related
to Uncore events. The Uncore counters measure per socket. Therefore
likwid-perfctr has a socket lock which ensures that only one thread per socket
starts the counters and only one thread per socket stops them. The first thread
arriving in start or stop gets the lock.

In a threaded context the output looks like that:

```
+--------------------------+------------+----------+----------+----------+
|          Metric          |   core 0   |  core 1  |  core 2  |  core 3  |
+--------------------------+------------+----------+----------+----------+
|       Runtime [s]        |  0.321233  | 0.320292 | 0.320335 | 0.320349 |
|       Clock [MHz]        |   2933.4   |  2933.4  |  2933.4  |  2933.4  |
|           CPI            |  4.32201   | 4.14965  | 4.14298  | 4.15057  |
| DP MFlops/s (DP assumed) |  195.277   | 150.988  | 150.965  | 150.967  |
|      Packed MUOPS/s      |  97.6377   | 75.4941  | 75.4827  | 75.4835  |
|      Scalar MUOPS/s      | 0.00218649 |    0     |    0     |    0     |
|        SP MUOPS/s        |     0      |    0     |    0     |    0     |
|        DP MUOPS/s        |  97.6398   | 75.4941  | 75.4827  | 75.4835  |
+--------------------------+------------+----------+----------+----------+
+-------------------------------+------------+------------+----------+-------------+
|            Metric             |    Sum     |    Max     |   Min    |     Avg     |
+-------------------------------+------------+------------+----------+-------------+
|       Runtime [s] STAT        |  1.28221   |  0.321233  | 0.320292 |  0.320552   |
|       Clock [MHz] STAT        |  11733.6   |   2933.4   |  2933.4  |   2933.4    |
|           CPI STAT            |  16.7652   |  4.32201   | 4.14298  |   4.1913    |
| DP MFlops/s (DP assumed) STAT |  648.198   |  195.277   | 150.965  |   162.05    |
|      Packed MUOPS/s STAT      |  324.098   |  97.6377   | 75.4827  |   81.0245   |
|      Scalar MUOPS/s STAT      | 0.00218649 | 0.00218649 |    0     | 0.000546622 |
|        SP MUOPS/s STAT        |     0      |     0      |    0     |      0      |
|        DP MUOPS/s STAT        |   324.1    |  97.6398   | 75.4827  |   81.025    |
+-------------------------------+------------+------------+----------+-------------+
```

For threaded measurements additional to the standard tables for every table an
additional statistic table is output including Sum, Max, Min and Avg for all
Event counts/metrics.

# Using custom event sets #

likwid-perfctr allows you to specify custom event sets. You can measure
as many events in one test run as there are physical counters on an architecture.
You specify the event set as a comma separated list of event/counter pairs.
This could look like:

```
likwid-perfctr  -c 0-3  -g FP_COMP_OPS_EXE_SSE_FP_PACKED:PMC0,UNC_L3_LINES_IN_ANY:UPMC0  likwid-pin -t intel  -c 0-3  ./stream-icc
```
with output (on Intel processors are automatically added to the event set enabling the connected derived metrics):
```
+-------------------------------+-------------+-------------+-------------+-------------+
|             Event             |   core 0    |   core 1    |   core 2    |   core 3    |
+-------------------------------+-------------+-------------+-------------+-------------+
|       INSTR_RETIRED_ANY       | 1.97831e+08 | 2.29654e+08 | 2.29902e+08 | 2.32312e+08 |
|     CPU_CLK_UNHALTED_CORE     | 9.18977e+08 | 9.20478e+08 | 9.20308e+08 | 9.19448e+08 |
| FP_COMP_OPS_EXE_SSE_FP_PACKED | 4.00249e+07 | 3.08977e+07 | 3.08971e+07 | 3.08893e+07 |
|      UNC_L3_LINES_IN_ANY      | 5.08051e+07 |      0      |      0      |      0      |
+-------------------------------+-------------+-------------+-------------+-------------+
+-------------+----------+----------+----------+----------+
|   Metric    |  core 0  |  core 1  |  core 2  |  core 3  |
+-------------+----------+----------+----------+----------+
| Runtime [s] | 0.313293 | 0.313804 | 0.313746 | 0.313453 |
|     CPI     | 4.64528  |  4.0081  | 4.00305  | 3.95782  |
+-------------+----------+----------+----------+----------+
```

# Performance groups #

For common tasks there exist pre-configured event sets. These groups provide
useful event sets and compute common derived metrics. We try to provide a basic
set of common groups on all architectures. Due to to the differing capabilities
some groups may be processor specific. You can print available groups on a
architecture with `./perfctr -a`. For processor specific information about what
events are chosen for the groups use the `-H -g group` switch. This gives you
detailed documentation from which events derived metrics are computed.

# Using the marker API #

The marker API allows you to measure named regions of your code. Overlap or
nesting of the regions is allowed. You can also enter a region multiple times,
e.g. in a loop. The counters for each region are accumulated. In the threaded case you can have
serial and threaded regions.

The marker API only reads out the counters. The configuration of the counters
is still handled via the wrapper application likwid-perfctr. In order to use
the likwid Marker API you must include the file likwid.h and link your code against
the library liblikwid.a (or its shared library variant if you compiled it) .
Additionally you need pthread enabled during linking.

For gcc or icc this look e.g. as:

```
 gcc -O3 -pthread -o test dofp.c -DLIKWID_PERFMON -L/usr/local/lib -llikwid -lm
```

Below is an example showing the usage of the marker API for a serial code:

```
#include <likwid.h>

likwid_markerInit();

likwid_markerStartRegion("Compute");
// Your code to measure
likwid_markerStopRegion("Compute");
likwid_markerClose();
```

For a threaded code it is important to call the following sequence of
function calls from the serial part of the program:

```
   likwid_markerInit();


   likwid_markerClose();
```

If you use the marker API together with the accessDaemon it is necessary
to also call an initialization routine in a parallel region for each thread:

```
   likwid_markerThreadInit();
```

To allow you to quickly toggle the marker API the likwid header contains a set
of macros which allow you to activate the marker API by defining `LIKWID_PERFMON`
during build of your software. You have to include the likwid header to your
source code to ensure your code also compiles if LIKWID is not available.

Example usage of the macro interface for threaded use:

```
#include <likwid.h>

LIKWID_MARKER_INIT;

// parallel part
LIKWID_MARKER_THREADINIT;
LIKWID_MARKER_START(“Compute”);
. . .
LIKWID_MARKER_STOP(“Compute”);


LIKWID_MARKER_START(“postprocess”);
. . .
LIKWID_MARKER_STOP(“postprocess”);

//serial part
LIKWID_MARKER_CLOSE;
```


For convenience there is also a simple API to pin your code or process or get
the processor id.

```
   likwid_getProcessorId();
```

# Using the marker API with Fortran 90 #

There is a native interface for using the likwid marker API with Fortran 90 programs. You have to enable it in the config.mk file as it is not enabled by default. If you enable it the Intel Fortran compiler flags are set. To change this to gfortran edit ./make/include\_GCC.mk to set gfortran with according flags.
You have to care that the fortran interface module likwid.mod is in your module include path and of course link against the likwid library.

For the Intel fortran compiler this can look as follows:

```
ifort -I../  -O3  -o fortran chaos.F90 -DLIKWID_PERFMON -L../ -llikwid  -lpthread -lm
```

There is a example how to use the marker API in Fortran in the test directory (chaos.F90).
Code example:
```
call likwid_markerInit()

call likwid_markerStart("sub")
! Do stuff
call likwid_markerStop("sub")

call likwid_markerClose()
```

The same rules apply as for the C variant.

# Defining custom performance groups #

With recent versions of likwid it is easy to specify your own performance
groups or change existing ones. All groups are specified in terms of text files
in the directory ./groups/ARCH/ (where ARCH is the processor microarchitecture)
and are named as the files. Adding a new group or changing an existing group is
nothing more than editing a text file. The format is explained best on an
example:

```
SHORT Double Precision MFlops/s

EVENTSET
FIXC0 INSTR_RETIRED_ANY
FIXC1 CPU_CLK_UNHALTED_CORE
PMC0  FP_COMP_OPS_EXE_SSE_FP_PACKED
PMC1  FP_COMP_OPS_EXE_SSE_FP_SCALAR
PMC2  FP_COMP_OPS_EXE_SSE_SINGLE_PRECISION
PMC3  FP_COMP_OPS_EXE_SSE_DOUBLE_PRECISION

METRICS
Runtime [s] FIXC1*inverseClock
CPI  FIXC1/FIXC0
DP MFlops/s (DP assumed) 1.0E-06*(PMC0*2.0+PMC1)/time
Packed MUOPS/s   1.0E-06*PMC0/time
Scalar MUOPS/s 1.0E-06*PMC1/time
SP MUOPS/s 1.0E-06*PMC2/time
DP MUOPS/s 1.0E-06*PMC3/time

LONG
Double Precision MFlops/s
```

The order of the statements is important. The first tag marks a short
description of the group. Then follows a list of events which are
measured. Of course only as many events as there are physical counters on an
architecture can be measured. First comes the Performance counter and then
separated by spaces the event. The supported events can be e.g. taken from the
list printed with the `-e` flag. After the `METRICS` tag a list of derived metrics,
one metric per line is specified. Every metric is made up of a formula
(without spaces) and an short description (as it will appear in the table). The
formula must follow C syntax. Preset variables which can be used in a metric is
`time` for the runtime and `inverseClock` for the inverse clock of the current
processor. After altering or adding a group the code must be rebuild to take effect.

# The timeline mode #

likwid-perfctr allows to measure a time resolved profile. With

```
likwid-perfctr -c N:0-7 -g CLOCK -d 2 > out.txt
```

you can measure the clock of turbo mode enabled Nehalem machines on logical
cores 0-7 with a measurement every 2 seconds. This means the counters will run
and every 2 seconds they will be read out. This is implemented in a very
lightweight fashion and should result in near to no overhead for your
application. The output is to stdout. It makes sense to pipe into a file. The
format of the output is one line for every event/metric, the first column is
the runtime in seconds from start. Following columns are the cores in the order
specified on the command line. To graph a specific event just grep the event
from this text file.

# The stethoscope mode #

likwid-perfctr allows you to listen for a specific time what is happening on a
node. This is useful if you want to look what a long running application
currently makes in terms of performance. We use it to profile MPI codes, where
we probably do not have access to the code. Stethoscope mode is also suited to
be used for monitoring. Still be careful to rely too much on these
measurements. Because you do not know what your code is actually doing it may
happen that the result is volatile depending which time period you were
measuring. Still it can give you a first idea what is going on with regard to
basic performance properties.

```
likwid-perfctr -c N:0-7 -g FLOPS_DP  -S 10
```


# Output filters #

You can use the option -o to specify output to a file. As described in the next
section this file can also include placeholders for things as pid or MPI rank.
You must also give a file extension and here comes the new output subsystem of
LIKWID into play. If you specify `.txt` as suffix the raw output is written to
this file. If you specify another suffix likwid-perfctr will write the output
to a temporary file and call a script with the name of the suffix to convert
the output to an arbitrary format or apply filtering of results. In the LIKWID
tree all filters are located in the filters directory. At the moment there are
examples for comma separated values (csv) and XML output. You can add further
output filters by just adding new scripts to this directory. My scripts use
perl but you can of course use any scripting language.

This allows you to tailor the output of likwid-perfctr, so that it fits well
into your tool chain. There is also a switch for directly generating CSV output
without calling a script. This is useful if likwid-perctr is used as
monitoring backend.

# Using likwid-perfctr for MPI programs #

To use likwid-perfctr for a MPI program the most important issue is to care for
the pinning of the processes to cores and to instruct likwid-perfctr which core
belong to which process. The current solution to this problem is to pin the MPI
process with a taskset and  call likwid-perfctr with `-c L:0` notation to
enable logical pinning inside this cpuset. In order to distinguish the output
for multiple processes the `-o` option allows to output all results to a file.

The filename can include placeholders separated by underscores, no other underscores are allowed in the filename:

  * `%j` - PBS\_JOBID taken from environment
  * `%r` - MPI Rank as specified by newer Intel MPI versions
  * `%h` - hostname
  * `%p` - process pid

The output filename is specified as:

```
likwid-perfctr -c L:0 -g FLOPS_DP -o test_%h_%p.txt  ./a.out
```

LikwidMpirun is a mpi startup wrapper which has builtin support for likwid-perfctr
measurements.