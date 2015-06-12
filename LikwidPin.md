﻿#summary likwid-pin: Tool to pin threaded applications without touching the source code



# NOTICE #

You can only use likwid-pin with threading implementations using the
`pthread_create` API call which are dynamically linked. Moreover the usage
makes only sense if you use a static placement of the threads. This means every thread
runs on a dedicated processor. Since version 3.1 it is possible to oversubscribe processors creating many more threads as there are processors. likwid-pin will distribute the threads round robin on the processors you specify in your thread list.

# Introduction #

For threaded applications on modern multi-core platforms it is crucial to pin
threads to dedicated cores. While the Linux kernel offers an API to pin your
threads it is tedious and involves some coding to implement a flexible solution
to address affinity. Intel includes an sophisticated pinning mechanism for
their OpenMP implementation. While this already works quite well out of the box
it can be further controlled with environment variables.

Still there are occasions where a simple platform and compiler independent
solution is required. Because all common OpenMP implementations rely on the
pthread API it is possible for likwid-pin to preload a wrapper library to the
pthread\_create call. In this wrapper the threads are pinned using the Linux OS
API. likwid-pin can also be used to pin serial applications as a replacement
for taskset. This is an idea inspired by a tool available at
> http://www.mulder.franken.de/workstuff/.

likwid-pin explicitly supports pthread and the OpenMP implementations of Intel
> and GNU gcc. Other OpenMP implementations are also supported by allowing to
specify a skip mask. In this mask it is specified which threads shall be
skipped during pinning because they are used as shepard threads and do no
actual work.

likwid-pin offers three different syntax flavors to specify how to pin threads to processors:

  1. Using a thread list
  1. Specify a expression based thread list
  1. Use scatter policy

Usually processors are numbered within the linux kernel, we refer to this ordering as physical numbering.
LIKWID introduces thread groups throughout all tools to enable logical pinning. A thread group are processors sharing a topological entity on a node or chip. This may be the socket, or a ccNUMA domain or a shared cache.
likwid-pin supports four different ways of numbering the cores when using the thread group syntax:

  1. **physical numbering**: processors are numbered according to the numbering in the OS
  1. **logical numbering in node**: processors are logical numbered over whole node (N prefix)
  1. **logical numbering in socket**: processors are logical numbered in every socket (S# prefix, e.g., S0)
  1. **logical numbering in cache group**: processors are logical numbered in last level cache group (C# prefix, e.g., C1)
  1. **logical numbering in memory domain**: processors are logical numbered in NUMA domain (M# prefix, e.g., M2)
  1. **logical numbering within cpuset**: processors are logical numbered inside Linux cpuset (L prefix)

For all numberings apart from one and six physical cores come first. If you
have two sockets with 4 cores each and every core has 2 SMT threads with `-c
N:0-7` you get all physical cores. To also use SMT threads use `N:0-15`.

Since version 3.1 LIKWID also supports an alternative expression based syntax variant.
If you use an expression based thread list definition compact ordering is used. So the processors will be in consecutive
ordering with regard to SMT threads.

likwid-pin can be used to also set the numa memory policy to interleave.
Because likwid-pin can figure out all memory domains involved in your run it
automatically configure interleaving for all numa nodes used in your run.

likwid-pin sets the environment variable OMP\_NUM\_THREADS for you if not already
present in your environment. It will set as many threads as present in your pin
expression.

# Options #
```
-h                  print a help message
-v                  Version information
-c thread list   Can be a physical or logical list or a thread expression or a scatter policy.  See below for details.
-S                  Sweep memory in involved numa nodes
-s skip mask        Specify a skip mask as hex number. The threads corresponding to the bits set are skipped.
-i                  Set numa interleave policy for all involved numa nodes
-q                  Silent execution with no output
-p                  Print thread domains. Using this thread together with  the -c option will output the thread list converted to physical processor Ids.
-d                  Specify custom delimiter if using likwid-pin to convert logical to physical Ids. Default is comma separated.
```

# Usage #

As usual you can get a short help message with
```
 likwid-pin -h
```

With a pthread application type (in this example with 4 threads)
```
 likwid-pin -c 0,2,4-6  ./myApp parameters
```

With pthread it is important that you also have to include the process in your processor list.
This is because for pthreads it is also possible to use the process as a worker.
You can omit the -c option now. likwid-pin will then automatically use -c N:0-maxProcessors.

For a gcc  OpenMP application this is the same. If you omit to set
`OMP_NUM_THREADS` likwid-pin will set it to as many threads as you specified in
your pinning expression.
```
 likwid-pin -c 0,2,4,6  ./myApp parameters
```

With logical numbering this may translate to:
```
 likwid-pin -c N:0-3  ./myApp parameters
```
or:
```
 likwid-pin  -c S0:0-3  ./myApp parameters
```
If you want the ccNUMA domains your threads are running to be cleaned up
before your code running you can use the `-S` flag:
```
 likwid-pin -S -c S0:0-3  ./myApp parameters
```

You can use multiple thread domains in a logical processor list, separated by `@`:
```
 likwid-pin -c S0:0-3@S3:4-7  ./myApp parameters
```

To print out available thread domains use ( the output is for a four socket
Nehalem EX machine). In this example socket, last level cache group and memory
domain are equivalent:
```
 $likwid-pin  -p
Domain 0:
        Tag N: 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63
Domain 1:
        Tag S0: 0 1 2 3 4 5 6 7 32 33 34 35 36 37 38 39
Domain 2:
        Tag S1: 8 9 10 11 12 13 14 15 40 41 42 43 44 45 46 47
Domain 3:
        Tag S2: 16 17 18 19 20 21 22 23 48 49 50 51 52 53 54 55
Domain 4:
        Tag S3: 24 25 26 27 28 29 30 31 56 57 58 59 60 61 62 63
Domain 5:
        Tag C0: 0 1 2 3 4 5 6 7 32 33 34 35 36 37 38 39
Domain 6:
        Tag C1: 8 9 10 11 12 13 14 15 40 41 42 43 44 45 46 47
Domain 7:
        Tag C2: 16 17 18 19 20 21 22 23 48 49 50 51 52 53 54 55
Domain 8:
        Tag C3: 24 25 26 27 28 29 30 31 56 57 58 59 60 61 62 63
Domain 9:
        Tag M0: 0 1 2 3 4 5 6 7 32 33 34 35 36 37 38 39
Domain 10:
        Tag M1: 8 9 10 11 12 13 14 15 40 41 42 43 44 45 46 47
Domain 11:
        Tag M2: 16 17 18 19 20 21 22 23 48 49 50 51 52 53 54 55
Domain 12:
        Tag M3: 24 25 26 27 28 29 30 31 56 57 58 59 60 61 62 63
```

For sweeping up all memory domains used in you pinning expression you can use
the `-S` flag. For details about why you want to sweep the memory look
[here](LikwidMemsweeper.md).

```
$likwid-pin  -c S0:0@S3:0 -S ./stream-icc

Sweeping memory
Sweeping domain 0: Using 104849 MB of 131062 MB
Sweeping domain 3: Using 104858 MB of 131072 MB
```

Starting from version 3.1 likwid-pin also supports thread expressions.

Expressions based thread list generation with compact processor numbering.
Example usage expression: likwid-pin -c E:N:8 ./myApp
This will generate a compact list of thread to processor mapping for the node domain with eight threads.
The following syntax variants are available:
  1. -c E:<thread domain>:<number of threads>
> 2. -c E:<thread domain>:<number of threads>:<chunk size>:

&lt;stride&gt;


> > For two SMT threads per core on a SMT 4 machine use e.g. -c E:N:122:2:4

The simplest way to use the expression based syntax is:

```
 likwid-pin -c E:S0:4  ./myApp parameters
```

This will use 4 processors within the socket 0 thread domain. Remember that the ordering is compact. This means if the processor has 2-way SMT the first two physical cores will be used with 4 threads.

Optionally you may specify a block size and stride:

```
 likwid-pin -c E:S0:8:1:2  ./myApp parameters
```

On a 2-way SMT system this is equivalent to `-c S0:0-7`, Eight threads, block size is one and stride (from start of block to start of block) is two. This is handy especially on systems with 4-way SMT. Consider a Xeon Phi, you want to use 2 SMT threads per physical core with only 30 cores resulting in 60 threads. This can easily be achieved with:

```
 likwid-pin -c E:N:60:2:4  ./myApp parameters
```

Or consider an AMD bulldozer system and you want to use only one core per FPU:

```
 likwid-pin -c E:S0:4:1:2  ./myApp parameters
```

You may also chain expression using the following syntax:

```
 likwid-pin -c E:S0:20:2:4@S1:4:1:2  ./myApp parameters
```

Another option is to use a scatter policy among a thread domain type.
Example usage scatter: likwid-pin -c M:scatter ./myApp
This will generate a thread to processor mapping scattered among all memory domains with physical cores first.

You can also use likwid-pin to convert logical thread expressions into physical processor lists. This may be handy for other tools which do not support logical processor Ids. Optional you moreover can specify a custom delimiter for this list with the -d option.

Since version 3.1 oversubscription is allowed reusing the thread list you provided. If an overflow occurred this will be indicated in the output.

# Example #

Example output for a OpenMP threaded STREAM benchmark.

```
$likwid-pin  -c 0-3  ./STREAM_OMP-WOODY
[likwid-pin] Main PID -> core 0 - OK
-------------------------------------------------------------
STREAM version $Revision: 5.8 $
-------------------------------------------------------------
This system uses 8 bytes per DOUBLE PRECISION word.
-------------------------------------------------------------
Array size = 6000000, Offset = 0
Total memory required = 137.3 MB.
Each test is run 10 times, but only
the *best* time for each is used.
-------------------------------------------------------------
[pthread wrapper] [pthread wrapper] PIN_MASK: 0->1  1->2  2->3
[pthread wrapper] SKIP MASK: 0x2
[pthread wrapper 0] Notice: Using libpthread.so.0
        threadid 47223170505040 -> core 1 - OK
[pthread wrapper 1] Notice: Using libpthread.so.0
        threadid 47223174703440 -> SKIP
[pthread wrapper 2] Notice: Using libpthread.so.0
        threadid 47223178901840 -> core 2 - OK
[pthread wrapper 3] Notice: Using libpthread.so.0
        threadid 47223183100240 -> core 3 - OK
Number of Threads requested = 4
-------------------------------------------------------------
Printing one line per active thread....
Printing one line per active thread....
Printing one line per active thread....
Printing one line per active thread....
-------------------------------------------------------------
Your clock granularity/precision appears to be 2 microseconds.
Each test below will take on the order of 70298 microseconds.
   (= 35149 clock ticks)
Increase the size of the arrays if this shows that
you are not getting at least 20 clock ticks per test.
-------------------------------------------------------------
WARNING -- The above is only a rough guideline.
For best results, please be sure you know the
precision of your system timer.
-------------------------------------------------------------
Function      Rate (MB/s)   Avg time     Min time     Max time
Copy:        7034.1035       0.0137       0.0136       0.0137
Scale:       7087.4672       0.0138       0.0135       0.0154
Add:         7147.0976       0.0207       0.0201       0.0219
Triad:       7186.9842       0.0207       0.0200       0.0227
-------------------------------------------------------------
Solution Validates
-------------------------------------------------------------
```