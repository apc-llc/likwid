# Introduction #

Add your content here.


# Test machine #

Determined by `likwid-topology -c -g`:

```
-------------------------------------------------------------
CPU type:	AMD Magny Cours processor 
*************************************************************
Hardware Thread Topology
*************************************************************
Sockets:		2 
Cores per socket:	8 
Threads per core:	1 
-------------------------------------------------------------
HWThread	Thread		Core		Socket
0		0		0		0
1		0		0		1
2		0		1		0
3		0		1		1
4		0		2		0
5		0		2		1
6		0		3		0
7		0		3		1
8		0		4		0
9		0		4		1
10		0		5		0
11		0		5		1
12		0		6		0
13		0		6		1
14		0		7		0
15		0		7		1
-------------------------------------------------------------
Socket 0: ( 0 2 4 6 8 10 12 14 )
Socket 1: ( 1 3 5 7 9 11 13 15 )
-------------------------------------------------------------

*************************************************************
Cache Topology
*************************************************************
Level:	 1
Size:	 64 kB
Type:	 Data cache
Associativity:	 2
Number of sets:	 512
Cache line size: 64
Non Inclusive cache
Shared among 1 threads
Cache groups:	( 0 ) ( 2 ) ( 4 ) ( 6 ) ( 8 ) ( 10 ) ( 12 ) ( 14 ) ( 1 ) ( 3 ) ( 5 ) ( 7 ) ( 9 ) ( 11 ) ( 13 ) ( 15 )
-------------------------------------------------------------
Level:	 2
Size:	 512 kB
Type:	 Unified cache
Associativity:	 16
Number of sets:	 512
Cache line size: 64
Non Inclusive cache
Shared among 1 threads
Cache groups:	( 0 ) ( 2 ) ( 4 ) ( 6 ) ( 8 ) ( 10 ) ( 12 ) ( 14 ) ( 1 ) ( 3 ) ( 5 ) ( 7 ) ( 9 ) ( 11 ) ( 13 ) ( 15 )
-------------------------------------------------------------
Level:	 3
Size:	 5 MB
Type:	 Unified cache
Associativity:	 96
Number of sets:	 512
Cache line size: 64
Non Inclusive cache
Shared among 4 threads
Cache groups:	( 0 2 4 6 ) ( 8 10 12 14 ) ( 1 3 5 7 ) ( 9 11 13 15 )
-------------------------------------------------------------

*************************************************************
NUMA Topology
*************************************************************
NUMA domains: 4 
-------------------------------------------------------------
Domain 0:
 Processors:  0 2 4 6
Memory: 31414.3 MB free of total 32763.7 MB
-------------------------------------------------------------
Domain 1:
 Processors:  8 10 12 14
Memory: 31707.9 MB free of total 32768 MB
-------------------------------------------------------------
Domain 2:
 Processors:  9 11 13 15
Memory: 31728.7 MB free of total 32768 MB
-------------------------------------------------------------
Domain 3:
 Processors:  1 3 5 7
Memory: 31694.3 MB free of total 32768 MB
-------------------------------------------------------------

*************************************************************
Graphical:
*************************************************************
Socket 0:
+---------------------------------------------------------------------------------+
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| |   0   | |   2   | |   4   | |   6   | |   8   | |   10  | |   12  | |   14  | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------------------------------------+ +-------------------------------------+ |
| |                 5MB                 | |                 5MB                 | |
| +-------------------------------------+ +-------------------------------------+ |
+---------------------------------------------------------------------------------+
Socket 1:
+---------------------------------------------------------------------------------+
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| |   1   | |   3   | |   5   | |   7   | |   9   | |   11  | |   13  | |   15  | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |  64kB | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | | 512kB | |
| +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ |
| +-------------------------------------+ +-------------------------------------+ |
| |                 5MB                 | |                 5MB                 | |
| +-------------------------------------+ +-------------------------------------+ |
+---------------------------------------------------------------------------------+
```

# Node bandwidth map #

With likwid-bench you can easily measure the bandwidth topology of a node. Above output
already tells us that the machine has four NUMA domains, two on each socket.

The Numa domains are:

```
Domain 0:
 Processors:  0 2 4 6
-------------------------------------------------------------
Domain 1:
 Processors:  8 10 12 14
-------------------------------------------------------------
Domain 2:
 Processors:  9 11 13 15
-------------------------------------------------------------
Domain 3:
 Processors:  1 3 5 7
```

The following results were generated with the `copy_mem` benchmarks which is a assembly memcpy using non temporal stores. This causes that the caches are more or less bypassed.
All loads are directly to L1 cache and also the stores go via WC buffers to main memory.
The benchmark runs use likwid-bench as follows:
```
likwid-bench -t copy_mem -g 1 -i 50 -w M0:1GB-0:M2,1:M2
```

Above example will place threads (all cores on a socket per default results in four) in the Memory domain 0, then for each stream the data placement can be specified. In this example both streams are placed in the memory domain 2. By that all combinations can be tested.


| **NODE** |  0  |  1  |  2  |  3  |
|:---------|:----|:----|:----|:----|
|   0      | 12163| 7279 | 7590 | 5831 |
|   1      | 7229 | 12203 | 5866 | 7574 |
|   2      | 7309 | 5761 | 12247 | 7505 |
|   3      | 5759 | 7404 | 7490  | 12570 |

You can roughly separate 3 different access domains: local DRAM (ca. 12GB/s), horizontal/vertical connections (7-7.5 GB/s) and cross connections (ca. 5.8 GB/s).
While you can measure a difference between the stronger connected link on the same socket and the vertical link between sockets, the difference in our measurements is not very large.

# Detect Numa problems in threaded codes #

likwid-perfctr offers a performance group NUMA on K10 based architectures. This group measures the requests (read/write) from the local NUMA node to all other NUMA nodes.
```
likwid-perfctr -c 0,8,1,9 -g NUMA  sleep 10
```
This call will measure the traffic between NUMA nodes on one core in each memory domain for 10 sec. . It is interesting that on this MagnyCours machine there is a constant traffic from all nodes to node 0. This was e.g. not the case on a IStanbul two socket system tested.

Ideally every node should only have traffic with itself. The following example shows the likwid-perfctr output a threaded memcpy code with correct first touch memory allocation:

```
./likwid-perfctr -c  0,8,1,9 -g NUMA   ./likwid-bench -t copy_mem -i 50 -g 2 -w M1:1GB -w M2:1GB
```

```
+------------------------------------+-------------+-------------+-------------+------------+
|               Metric               |   core 0    |   core 8    |   core 1    |   core 9   |
+------------------------------------+-------------+-------------+-------------+------------+
| Mega requests per second to Node 0 |   18.1797   |   1153.79   |   625.223   |  1188.88   |
| Mega requests per second to Node 1 | 0.000281602 |   118.518   | 0.000459883 | 0.00127894 |
| Mega requests per second to Node 2 | 0.00179433  | 0.00526875  | 0.00127301  |  118.453   |
| Mega requests per second to Node 3 | 0.00291742  | 0.000817404 | 0.000239104 | 0.00042742 |
+------------------------------------+-------------+-------------+-------------+------------+
```

```
+------------------------------------+-------------+------------+-------------+------------+
|               Metric               |   core 0    |   core 8   |   core 1    |   core 9   |
+------------------------------------+-------------+------------+-------------+------------+
| Mega requests per second to Node 0 |   17.7524   |  1168.27   |   233.312   |  1404.89   |
| Mega requests per second to Node 1 |  3.807e-05  | 0.0236263  | 0.00150415  | 0.00123362 |
| Mega requests per second to Node 2 | 1.29736e-05 | 0.00619037 | 0.000663708 |  94.9712   |
| Mega requests per second to Node 3 | 0.00129658  |  88.3973   |   2.91165   | 0.00283263 |
+------------------------------------+-------------+------------+-------------+------------+
```