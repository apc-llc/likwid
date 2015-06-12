

**Experimental**

# Introduction #

Pinning to dedicated compute resources is important for pure MPI and even more for hybrid MPI/threaded applications. While all major MPI implementations include their mechanism for pinning likwid-mpirun provides a simple and portable solution based on the powerful capabilities of likwid-pin. This is still experimental at the moment and works out of the box only for Intel Compiler 11 and Intel MPI 4.0 together with the PBS scheduler. Still it can be adopted to any MPI and OpenMP combination with the help of a tuning application in the test directory of likwid.

# Usage #

As usual you can get a help message with
```
 likwid-mpirun -h
```

You always have to specify the total number of MPI processes with the `-np NUMPROC`.
Two cases are distinguished: Pure MPI and hybrid applications.

Pure MPI:
```
likwid-mpirun -np 16 -- ./a.out
```

The double dash is necessary to prevent scanning of application arguments. This will start 16 processes, the number of processes per compute node are taken from the PBS node file. If ppn is eight, eight processes are pinned to cores/SMT threads per node. the pinning is implemented with the likwid-pin node domain.

Pure MPI with explicit pinning:
```
likwid-mpirun -np 16 -NperDomain S:2 -- ./a.out
```

For this case a single option `-NperDomain` covers all cases. The argument contains a domain character as already known from the other likwid applications and the number per domain separated by a colon. Above example will start two processes per socket and will pin the processes with likwid-pin.

Domains can be:

  * N - for node
  * S - for socket
  * C - for last level shared cache
  * M - for NUMA domain (interesting e.g. for AMD Magny Cours)

For pinning on Magny Cours the following can be useful:
```
likwid-mpirun -np 16 -NperDomain M:2 -- ./a.out
```

This will start 2 processes per NUMA domain. On a two socket MagnyCours system this will result in 8 processes per node with two nodes total for this run.

The script will create a hostfile in `/tmp` named `mpiexec-cfg.pid".
For debugging use the debug option:
```
likwid-mpirun -debug -np 16 -NperDomain M:2 -- ./a.out
```
This will output all command which would be executed. The generated config hostfile in /tmp will not be deleted.

Pinning of hybrid applications:
```
likwid-mpirun  -np 16 -pin S0:0,1_S1:0,1 -- ./a.out
```
Hybrid pinning has only one option covering all possibilities with `-pin`.
The argument string to pin consists of valid likwid-pin expressions separated by underscores. The number of separated expression denote the number of processes started
per node. Above example will start two processes per node. The first process and its threads (two) will be pinned to Socket one, core 0,1. The second process and its threads will be pinned to socket two, core 0,1. At the moment you have to set `OMP_NUM_THREADS` by hand. Future versions will extract this information from the pin string.

The complexity here is that the OpenMP  as well as the MPI implementaion could start their own threads for management purpose which need not to be pinned. The threads which need to be skipped have to be determined in advance. likwid-mpirun supports at the moment one scenario for Intel compiler 11 and Intel MPI 4. This can be set with option `-type intel`.
In the future more scenarios will be supported.

At the moment all pinning uses block distribution, round robin variants for node and global are planned.

# Options #

All options:
```
-np <NUMPROC> : number of MPI processes

Optional:
-help                  : this (help) message
-debug                 : debug run (only outputs commands without execution)
-NperDomain <argument> : Run specified number of processes per domain.
                         Supported domains are: 
                         N Node
                         S Socket
                         C last level cache group
                         M NUMA domain
-pin <argument>        : Specify pinning for hybrid execution.
                         Processes are separated by underscore.
                         The threaded pinning must be a valid likwid-pin list.
-type <argument>       : Enables support for specific hybrid setup. Use only
                         together with -pin option.
--                     : Stop the likwid-mpirun parser. Useful for saving options to
                         the MPI application.
```

# Tuning #