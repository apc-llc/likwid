﻿#summary likwid-memsweeper - A tool to cleanup ccNUMA domains



# Introduction #

To utilize the parallel memory bandwidth available on ccNUMA systems it is
necessary to load data mainly from local memory seen from the threads point of view.
While the operating system usually decides where a page is placed on Linux the
default page placement policy is first touch. This means that a memory page is
placed in the NUMA memory domain the thread which writes first to the page runs
in. By this software has explicit control where the data is placed.

Still first touch is only a hint where you want the page to be placed, the
operating system still can decide to place it elsewhere. This can for example
happen if the local NUMA domain is already full and there is space free in a
remote domain. This frequently happens if you or another user has accessed a
large file. To speed up subsequent access to files Linux maintains a so called
file buffer cache, which can consume a large part of the available memory. This
may cause your data to be placed in a remote domain even if you have employed
correct first touch placement.

There are multiple solutions to this problem. Root can execute a command to
drop the file buffer cache. You can use numactl tools or the belonging library
to enforce page placement. Still there is some danger here if you use no swap.
You can also allocate almost all of the physical memory and write to it which
will also cause the file buffer cache to be dropped. This is exactly what
likwid-memsweeper is doing. It allows you to clean up all or some of the ccNUMA
domains on a compute node in a safe and convenient way. This functionality is
also available as an option to likwid-pin.

Starting with version 3.1.2 of LIKWID, also the CPU caches of the selected node(s) are invalidated to avoid the time-consuming eviction of cache lines of different processes.

# Options #

```
-h Help message
-v Version information
-c specify NUMA domain ID to clean up
```

# Usage #

You can get a help message with
```
 likwid-memsweeper -h
```

To cleanup all ccNUMA domains of a node call:
```
 likwid-memsweeper
```

To cleanup a specific ccNUMA domains call:
```
 likwid-memsweeper -c
```