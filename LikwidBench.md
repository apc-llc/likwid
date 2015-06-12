

# Introduction #

likwid-bench is a benchmarking application together with a framework to enable
rapid prototyping of multi-threaded assembly kernels. Adding a new benchmark is
nothing more than to create a simple text file and recompile. The framework
cares for threaded execution and pinning, data allocation and placement, time
measurement and result presentation.

# Build #

Because likwid-bench uses x86-64 instructions in its benchmarks kernels and to
enable that the rest of likwid still compiles on a 32 bit architecture you need
to call a special make target to build likwid-bench. To build it call:

```
make likwid-bench
```

## Limitiations ##

likwid-bench supports up to 38 streams. Also notice that at them moment only
plains streams are supported. This makes it not possible to emulate the
behavior of multi dimensional data structures with their spatial locality.

# Usage #

likwid-bench out of the box has already a bunch of kernels included. You can
use it as a basic bandwidth benchmarking tool as it is.

You can get a help message with

```
likwid-bench -h
```

A list with all available benchmark kernels is available when calling:

```
likwid-bench -a
```

You have to specify a benchmark kernel you want to use. This kernel will
operate on a number of streams. Streams are one dimensional arrays (or
vectors). Lets assume you only use one workgroup (thread group), then all
threads of a workgroup will divide the stream in portions and every thread will
update its fraction of the total vector.

Each assembly kernel has a number of properties.
These are:
  1. Number of streams
  1. The data type (DOUBLE, SINGLE, INT)
  1. number of flops it performs in one update
  1. number of bytes it transfers in one update
  1. the stride of one loop iteration

To output the properties of a test kernel call likwid-bench as:
```
$ ./likwid-bench -l copy
Name: copy
Number of streams: 2
Loop stride: 8
Flops: 0
Bytes: 16
Data Type: Double precision float
```

You have to specify how many threads you want to use, where these threads
should be placed and how large the total data set should be the workgroup
operates on. Per default the memory is allocated in the same domain the threads
are running in, optionally you can place the memory in another domain. All
vectors are per default page aligned.

Lets try some examples to illustrate this.
Get the default list of benchmark kernels:

```
% ./likwid-bench -a
clcopy
clload
clstore
copy
copy_mem
load
store
store_mem
stream
stream_mem
triad
triad_mem
```

In order to specify the number of threads and where these threads should be
placed we already used the term thread domain. A thread domain is a number of
threads sharing a topological entity. This can be a socket or a shared cache or
a NUMA domain.

To get a list of thread domains call:

```
$./likwid-bench  -p
Domain 0:
        Tag S0: 0 1 2 3 4 5
Domain 1:
        Tag S1: 6 7 8 9 10 11
Domain 2:
        Tag C0: 0 1 2 3 4 5
Domain 3:
        Tag C1: 6 7 8 9 10 11
```

This a Intel Westmere EP with two sockets. There is a shared L3 cache which is
equivalent to the socket domains. There are two socket groups S0 and S1 and two
cache groups C0 and C1. Notice that likwid-bench at the moment only considers
physical cores. SMT threads are ignored at the moment, this might change in the
future. One further limitation is that only last level caches are considered.

The simplest form to run a benchmark is:

```
$./likwid-bench  -t copy -g 1  -w S1:100kB
Allocate: Process running on core 6 - Vector length 6400 Offset 0
Allocate: Process running on core 6 - Vector length 6400 Offset 0
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: copy
-------------------------------------------------------------
Using 1 work groups
Using 6 threads
-------------------------------------------------------------
Group: 0 Thread 5 Global Thread 5 running on core 11 - Vector length 1064 Offset 5320
Group: 0 Thread 2 Global Thread 2 running on core 8 - Vector length 1064 Offset 2128
Group: 0 Thread 4 Global Thread 4 running on core 10 - Vector length 1064 Offset 4256
Group: 0 Thread 0 Global Thread 0 running on core 6 - Vector length 1064 Offset 0
Group: 0 Thread 3 Global Thread 3 running on core 9 - Vector length 1064 Offset 3192
Group: 0 Thread 1 Global Thread 1 running on core 7 - Vector length 1064 Offset 1064
Cycles: 91272 
Iterations: 100 
Size: 6400 
Vectorlength: 1064 
Time: 3.111599e-05 sec
MFlops/s:       0.00
MByte/s:        329091.30
Cycles per update:      0.857820
Cycles per cacheline:   6.862556
-------------------------------------------------------------
```

This example used the copy kernel and run it on socket 1 with all threads
available there. The working set size is set to 100 kB (Unit can be either kB,
MB or GB).You get a output where the streams are placed and how the threads are
pinned and and on what part of the vector each thread operates. Per default 100
iterations are performed. The tool reports beyond runtime the flop rate (if
applicable) and the bandwidth in MB/s. Also reported is the cycles to perform
one update and the cycles to update a cacheline.

**NOTICE:**
The cycles are RDTSC cycles. On modern processors with Turbo mode the RDTSC clock
is invariant. This means that it can be different from the actual clock.
To make the cycles metrics meaningful you have to fix the frequency to the nominal
frequency.

Let try a single threaded example with the stream benchmark in L1 cache:

```
$./likwid-bench  -t stream -g 1 -i 1000  -w S1:20kB:1
Allocate: Process running on core 6 - Vector length 853 Offset 0
Allocate: Process running on core 6 - Vector length 853 Offset 0
Allocate: Process running on core 6 - Vector length 853 Offset 0
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: stream
-------------------------------------------------------------
Using 1 work groups
Using 1 threads
-------------------------------------------------------------
Group: 0 Thread 0 Global Thread 0 running on core 6 - Vector length 848 Offset 0
Cycles: 870227 
Iterations: 1000 
Size: 853 
Vectorlength: 848 
Time: 2.966629e-04 sec
MFlops/s:       5750.64
MByte/s:        69007.63
Cycles per update:      1.026211
Cycles per cacheline:   8.209689
-------------------------------------------------------------
```

A workgroup is specified with `<domain>:<size>:[<threads>]` . The number of
threads is optional. Time is measured by global thread 0. An efficient spin
waiting loop based barrier is employed to keep the overhead low.

The following example will do the same as above, but this time with two
workgroups on two different sockets. Notice that also the memory is placed on
each of the sockets according to the workgroups.

```
$./likwid-bench  -t stream -g 2 -i 1000  -w S1:20kB:1 -w S0:20kB:1
Allocate: Process running on core 6 - Vector length 853 Offset 0
Allocate: Process running on core 6 - Vector length 853 Offset 0
Allocate: Process running on core 6 - Vector length 853 Offset 0
Allocate: Process running on core 0 - Vector length 853 Offset 0
Allocate: Process running on core 0 - Vector length 853 Offset 0
Allocate: Process running on core 0 - Vector length 853 Offset 0
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: stream
-------------------------------------------------------------
Using 2 work groups
Using 2 threads
-------------------------------------------------------------
Group: 0 Thread 0 Global Thread 0 running on core 0 - Vector length 848 Offset 0
Group: 1 Thread 0 Global Thread 1 running on core 6 - Vector length 848 Offset 0
Cycles: 931891 
Iterations: 1000 
Size: 853 
Vectorlength: 848 
Time: 3.176843e-04 sec
MFlops/s:       10740.22
MByte/s:        128882.66
Cycles per update:      1.098928
Cycles per cacheline:   8.791425
-------------------------------------------------------------
```

There is also the possibility to further specify in more detail how the memory
should be allocated and placed. Per default every stream is allocated page
aligned in the same domain the threads run in. You can change this with the
following optional arguments:

```
$./likwid-bench  -t copy -g 2 -i 60  -w S1:1GB:2-0:S0,1:S0  -w S0:1GB:2
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: copy
-------------------------------------------------------------
Using 2 work groups
Using 4 threads
-------------------------------------------------------------
Group: 0 Thread 1 Global Thread 1 running on core 1 - Vector length 33554432 Offset 33554432
Group: 0 Thread 0 Global Thread 0 running on core 0 - Vector length 33554432 Offset 0
Group: 1 Thread 1 Global Thread 3 running on core 7 - Vector length 33554432 Offset 33554432
Group: 1 Thread 0 Global Thread 2 running on core 6 - Vector length 33554432 Offset 0
Cycles: 41084567862 
Iterations: 60 
Size: 67108864 
Vectorlength: 33554432 
Time: 1.400605e+01 sec
MFlops/s:       0.00
MByte/s:        9199.52
Cycles per update:      20.406926
Cycles per cacheline:   163.255405
-------------------------------------------------------------
```

This example runs two reads per socket on the copy kernel but overrides the
default setting with placing all vectors in the socket 0 domain. Notice that
you either specify no stream arguments or all stream arguments. This means that
if your kernel operated on two stream you have to specify two streams in the
optional memory arguments. The syntax is
`<domain>:<size>:[<threads>]-<stream>:<domain>:<offset>` . You can offset
the array by a multiple of type. If the kernel operated on doubles you can
offset the array by a multiple of doubles. Notice that this offset is also
checked against the stride of the loop. Offsetting can be of advantage if
you think you have associativity problems.

Of course this is not too smart on a NUMA machine. If placing the data
correctly and using all threads with the kernel employing non temporal stores
you get the peak memory bandwidth of this system:

```
$./likwid-bench  -t copy_mem -g 2 -i 100  -w S1:1GB  -w S0:1GB  
Allocate: Process running on core 6 - Vector length 67108864 Offset 0
Allocate: Process running on core 6 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: copy_mem
-------------------------------------------------------------
Using 2 work groups
Using 12 threads
-------------------------------------------------------------
Group: 0 Thread 1 Global Thread 1 running on core 1 - Vector length 11184808 Offset 11184808
Group: 1 Thread 2 Global Thread 8 running on core 8 - Vector length 11184808 Offset 22369616
Group: 1 Thread 0 Global Thread 6 running on core 6 - Vector length 11184808 Offset 0
Group: 0 Thread 0 Global Thread 0 running on core 0 - Vector length 11184808 Offset 0
Group: 1 Thread 4 Global Thread 10 running on core 10 - Vector length 11184808 Offset 44739232
Group: 1 Thread 1 Global Thread 7 running on core 7 - Vector length 11184808 Offset 11184808
Group: 1 Thread 5 Global Thread 11 running on core 11 - Vector length 11184808 Offset 55924040
Group: 0 Thread 5 Global Thread 5 running on core 5 - Vector length 11184808 Offset 55924040
Group: 1 Thread 3 Global Thread 9 running on core 9 - Vector length 11184808 Offset 33554424
Group: 0 Thread 2 Global Thread 2 running on core 2 - Vector length 11184808 Offset 22369616
Group: 0 Thread 4 Global Thread 4 running on core 4 - Vector length 11184808 Offset 44739232
Group: 0 Thread 3 Global Thread 3 running on core 3 - Vector length 11184808 Offset 33554424
Cycles: 15602213015 
Iterations: 100 
Size: 67108864 
Vectorlength: 11184808 
Time: 5.318840e+00 sec
MFlops/s:       0.00
MByte/s:        40375.03
Cycles per update:      13.949469
Cycles per cacheline:   111.595750
-------------------------------------------------------------
```

# Default benchmarks #

likwid-bench already  contains a number of basic benchmark kernel you can use
out of the box.

These are:

  * **copy** Standard memcpy benchmark. `A[i] = B[i]`
  * **copy\_mem** The same as above but with non temporal store.
  * **load** One load stream. This one does some software prefetching you can experimenet with.
  * **store** One store stream.
  * **store\_mem** The same as above but with non temporal store.
  * **stream** Classical STREAM triad. `A[i] = B[i] + a * C[i]`.
  * **stream\_mem** The same as above but with non temporal store.
  * **triad** Full vector triad. `A[i] = B[i] + C[i] * D[i]`.
  * **triad\_mem**  The same as above but with non temporal store.

Apart from these standard benchmarks there are special cacheline versions for the basic data operations load, store and copy. These versions only execute one operation per cacheline. Thereby the runtime is as far as possible reduced to the time needed for the data transfers inside the memory hierarchy. Use this benchmarks to measure the raw bandwidth of different memory levels.

  * **clcopy**
  * **clload**
  * **clstore**


# Using likwid-bench together with likwid-perfctr #

To measure hardware performance counter events likwid-bench can be build to be
instrumented with the likwid marker API allowing to measure additional events.

To build likwid-bench for use with likwid-perfctr set the following switch
in config.mk to true:

```
INSTRUMENT_BENCH = true
```

call `make distclean` and rebuild. Now you can use both tools together. Of
course in likwid-perfctr you still have to specify the cores you want to
measure explicitly. To indicate that likwid-bench was build with
instrumentation it will output a message `Using likwid`.

The following measurements shows a multi socket Uncore measurement for the L3
cache with 2 threads running on each socket:

```
$likwid-perfctr -c 0,1,6,7 -g L3CACHE likwid-bench  -t copy_mem -g 2 -i 100  -w S1:1GB:2  -w S0:1GB:2
Speedstep is enabled!
This produces inaccurate timing measurements.
For reliable clock measurements disable speedstep.
-------------------------------------------------------------
CPU type:       Intel Core Westmere processor 
CPU clock:      2.93 GHz 
-------------------------------------------------------------
Measuring group L3CACHE
-------------------------------------------------------------
Allocate: Process running on core 6 - Vector length 67108864 Offset 0
Allocate: Process running on core 6 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Allocate: Process running on core 0 - Vector length 67108864 Offset 0
Using likwid
-------------------------------------------------------------
LIKWID MICRO BENCHMARK
Test: copy_mem
-------------------------------------------------------------
Using 2 work groups
Using 4 threads
-------------------------------------------------------------
Group: 1 Thread 1 Global Thread 3 running on core 7 - Vector length 33554432 Offset 33554432
Group: 1 Thread 0 Global Thread 2 running on core 6 - Vector length 33554432 Offset 0
Group: 0 Thread 1 Global Thread 1 running on core 1 - Vector length 33554432 Offset 33554432
Group: 0 Thread 0 Global Thread 0 running on core 0 - Vector length 33554432 Offset 0
Cycles: 31388820498 
Iterations: 100 
Size: 67108864 
Vectorlength: 33554432 
Time: 1.070056e+01 sec
MFlops/s:       0.00
MByte/s:        20068.89
Cycles per update:      9.354597
Cycles per cacheline:   74.836780
-------------------------------------------------------------
+-----------------------+-------------+-------------+-------------+-------------+
|         Event         |   core 0    |   core 1    |   core 6    |   core 7    |
+-----------------------+-------------+-------------+-------------+-------------+
|   INSTR_RETIRED_ANY   | 5.40253e+09 | 5.45509e+09 | 4.1945e+09  | 4.19677e+09 |
| CPU_CLK_UNHALTED_CORE | 3.33546e+10 | 3.35159e+10 | 3.35228e+10 | 3.35342e+10 |
|    UNC_L3_HITS_ANY    | 3.82275e+07 |      0      | 3.86728e+07 |      0      |
|    UNC_L3_MISS_ANY    |  1.716e+09  |      0      | 1.71604e+09 |      0      |
|  UNC_L3_LINES_IN_ANY  | 8.47763e+08 |      0      | 8.46451e+08 |      0      |
| UNC_L3_LINES_OUT_ANY  | 8.47762e+08 |      0      | 8.46451e+08 |      0      |
+-----------------------+-------------+-------------+-------------+-------------+
+-----------------+------------+--------+------------+--------+
|     Metric      |   core 0   | core 1 |   core 6   | core 7 |
+-----------------+------------+--------+------------+--------+
| L2 request rate | 0.00707585 |   0    | 0.00921989 |   0    |
|  L2 miss rate   |  0.31763   |   0    |  0.409117  |   0    |
|  L2 miss ratio  |  44.8893   |   0    |  44.3733   |   0    |
+-----------------+------------+--------+------------+--------+
```

For uncore events likwid-perfCtr will only measure on one core per socket.

# Adding benchmarks #

To add new benchmarks you have to create test files the directory `./bench` .
The file must have the ending `.ptt`. Lets look on a copy benchmark `copy.ptt`.
Later the benchmark will be name according to the filename.

```
STREAMS 2
TYPE DOUBLE
FLOPS 0
BYTES 16
LOOP 8
movaps    FPR1, [STR0 + GPR1 * 8]
movaps    FPR2, [STR0 + GPR1 * 8 + 16]
movaps    FPR3, [STR0 + GPR1 * 8 + 32]
movaps    FPR4, [STR0 + GPR1 * 8 + 48]
movaps    [STR1 + GPR1 * 8]     , FPR1
movaps    [STR1 + GPR1 * 8 + 16], FPR2
movaps    [STR1 + GPR1 * 8 + 32], FPR3
movaps    [STR1 + GPR1 * 8 + 48], FPR4
```

The file consists of a header section and the actual loop kernel. The following header tags must be present (the order is arbitrary):
  * `STREAM`: The number of streams the benchmark needs.
  * `TYPE`: Can be one of DOUBLE, SINGLE or INT.
  * `FLOPS`: How many flops the kernel executes in for one update.
  * `BYTES`: How many bytes need to be transfered per update.

Everything else before the `LOOP` tag are taken as instruction code and placed
before the actual loop code. Everything after `LOOP` is placed inside the loop
kernel. The argument behind `LOOP` indicates the stride of the loop, means how
many updates are performed in one loop iteration. The instruction code must be
in Intel syntax. You can write plain x86-64 instruction code, but likwid
provides some predefined labels to ease your job. For all registers special
labels exist, e.g. you can access for all SSE floating point registers the
label `FPR1-FPR16`, the same exists for the general purpose registers with
`FPR1-FPR14`, `esp` and `ebp` are not mapped. The streams you ordered are
accessible through special stream labels e.g. `STR0`. These stream labels are
just labels for general purpose registers holding the address on the array. As
loop index register `GPR1` is used which maps on `rax`. likwid also takes care
if more than six arguments need to be passed to the function and moves the
address to an appropriate register. Of course this approach limits the
maximum number of streams by the number of available general purpose
registers. At the moment at maximum 12 streams can be used in a kernel.

Technically the text files in the `ptt` format is converted in an intermediate
high level assembly format and finally to gas assembly. Both intermediate
formats, the `.pas` file and the `.s` are present in the build directory (e.g.
`./GCC`). The intermediate assembly format allows to provide different
assembler backends, e.g. for masm. Still at the moment there is only a backend
for gas.

After recompiling the benchmark code is generated and automatically included in
likwid-bench.

# Community Aspect #

One idea behind likwid-bench beyond the ability of rapid protyping and
benchmarking of loop kernels is to enable a platform which helps to generate
knowledge about what instructions code works on different platforms for certain
algorithms. We want e.g. provide learning packages with collections of micro
benchmarks showing the influence of different instructions and implementation
types on performance. Users can then easily share their implementations and
results can be easily compared on different processors. The typical targets for
such packages are the e.g. :

  * Stencil kernels: Jacobi, Gauss Seidel
  * Stream and Full triad (4 vectors)
  * Add operations
  * basic data operations (load, store, copy)


# Future Plans #

  * more data access patterns should be supported apart from plain streams. E.g. multidimensional arrays for stencil kernels or CRS data formats for sparse matrix computations.
  * provide more assembler backends.
  * Provide more example packages.
  * Provide a perl skript which generates a _bandwidth map_ based on likwid-bench measurements
