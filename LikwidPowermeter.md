

# Introduction #

Intel recently introduced an interface to configure and readout energy
consumption of processors and memory. This so called RAPL interface is
controlled through MSR registers. likwid-powermeter is a small tool which
allows you to query the energy consumed within a package for a given time
period and computes the resulting power consumption.

Additionally you can query the supported Turbo Mode steps of all Turbo mode
equipped processors (except the EX variants). This information is also queried
from MSR registers.

The RAPL counters are also available as events in likwid-perfctr. There is a ENERGY
group on Intel SandyBridge to measure common metrics.

**NOTICE** You have to setup access to the msr device files to use
likwid-powermeter.

# Examples #

As usual you can get a short help message with
```
 likwid-powermeter -h
```


Do get info about RAPL and Turbo Mode call
```
 likwid-powermeter -i
```

Toggle between the access modes of LIKWID to the MSR/RAPL counters:
```
 likwid-powermeter -M 0
```
-M 0 means directly accessing the MSR device files and -M 1 forward the read/write requests to LIKWID's accessDaemon

Output should be something like the following:
```
-------------------------------------------------------------
CPU name:       Intel Core SandyBridge processor 
CPU clock:      3.49 GHz 
-------------------------------------------------------------
Base clock:     3500.00 MHz 
Minimal clock:  1600.00 MHz 
Turbo Boost Steps:
C1 3900.00 MHz 
C2 3800.00 MHz 
C3 3700.00 MHz 
C4 3600.00 MHz 
-------------------------------------------------------------
Thermal Spec Power: 95 Watts 
Minimum  Power: 20 Watts 
Maximum  Power: 95 Watts 
Maximum  Time Window: 0.15625 micro sec 
-------------------------------------------------------------
```

This means the processor has a TDP of 95Watt. With 1 Core active it can
overclock up to 3.9 GHz. With all four cores active it still may overclock to
3.6 GHz.

To measure power in a given duration (Stethoscope mode) use
```
 likwid-powermeter -s 3
```

which gives you something like
```
-------------------------------------------------------------
CPU name:       Intel Core SandyBridge processor 
CPU clock:      3.49 GHz 
-------------------------------------------------------------
Measure on CoreId 0 
Runtime: 3 s 
Domain: PKG 
Energy consumed: 11.4889 Joules 
Power consumed: 3.82963 Watts 
```

Next you can use likwid-powermeter as a wrapper:
```
 likwid-powermeter  ./a.out
```

Finally you can also output the clock and CPI calues for the socket you are
currently measuring:

```
 likwid-powermeter -p ./a.out
```

It outputs a table similar to likwid-perfctr:

```
+-----------------------+-------------+-------------+--------+--------+
|         Event         |   core 0    |   core 1    | core 2 | core 3 |
+-----------------------+-------------+-------------+--------+--------+
|   INSTR_RETIRED_ANY   | 2.46061e+09 | 2.45852e+09 | 31496  |  3577  |
| CPU_CLK_UNHALTED_CORE | 2.68793e+09 | 2.68622e+09 | 74456  | 38276  |
| CPU_CLK_UNHALTED_REF  | 2.68808e+09 | 2.68622e+09 | 96145  | 57540  |
|    PWR_PKG_ENERGY     |     16      |      0      |   0    |   0    |
|    PWR_DRAM_ENERGY    |     16      |      0      |   0    |   0    |
+-----------------------+-------------+-------------+--------+--------+
+-----------------+---------+---------+---------+---------+
|     Metric      | core 0  | core 1  | core 2  | core 3  |
+-----------------+---------+---------+---------+---------+
|   Clock [MHz]   | 3491.17 | 3491.35 | 2703.76 | 2322.48 |
|       CPI       | 1.09238 | 1.09261 | 2.36398 | 10.7006 |
|   Energy [J]    |   16    |    0    |    0    |    0    |
|   Power [W]     | 15.3491 |    0    |    0    |    0    |
| Energy DRAM [J] |   16    |    0    |    0    |    0    |
| Power DRAM [W]  | 15.3491 |    0    |    0    |    0    |
+-----------------+---------+---------+---------+---------+
+----------------------+---------+---------+---------+-----------+
|        Metric        |   Sum   |   Max   |   Min   |    Avg    |
+----------------------+---------+---------+---------+-----------+
|   Clock [MHz] STAT   | 12008.8 | 3491.35 | 2322.48 |  3002.19  |
|       CPI STAT       | 15.2496 | 10.7006 | 1.09238 |  3.81239  |
| Energy [J] STAT      |   16    |   16    |    0    |    2      |
| Power [W] STAT       | 15.3491 | 15.3491 |    0    | 1.91864   |
| Energy DRAM [J] STAT |   16    |   16    |    0    |    2      |
| Power DRAM [W] STAT  | 15.3491 | 15.3491 |    0    | 1.91864   |
+----------------------+---------+---------+---------+-----------+
```

The application only used two cores and clocked (in average) 3.5 GHz.

Lets consider a more intensive run (shortend table):

```
+-------------+----------+---------+----------+----------+
|   Metric    |  core 0  | core 1  |  core 2  |  core 3  |
+-------------+----------+---------+----------+----------+
| Clock [MHz] |  3491.9  | 3491.92 | 3491.92  | 3491.92  |
|     CPI     | 0.641725 | 0.64253 | 0.642629 | 0.641353 |
+-------------+----------+---------+----------+----------+

Runtime: 10.8847 s 
Domain: PKG 
Energy consumed: 602.067 Joules 
Power consumed: 55.3131 Watts
```

Turbo mode was disabled on this machine.

For each package (socket) exist one instance of RAPL counters, hence the values can only be retrieved on a package basis. Single cores cannot be measured. In order to measure multiple packages (sockets) at once, the likwid-powermeter supports the -c cmdline switch:
```
 likwid-powermeter -c 0,1 -s 1
```

The values are printed for each package, no aggregation is done by LIKWID:

```
-------------------------------------------------------------
CPU name:	Intel Core SandyBridge EP processor 
CPU clock:	3.09 GHz 
-------------------------------------------------------------
Measure on sockets: 0, 1
Runtime: 1 second 
-------------------------------------------------------------
Socket 0
Domain: PKG 
Energy consumed: 15.1598 Joules 
Power consumed: 15.1598 Watts 
Domain: DRAM 
Energy consumed: 1.4343 Joules 
Power consumed: 1.4343 Watts 

Socket 1
Domain: PKG 
Energy consumed: 16.0223 Joules 
Power consumed: 16.0223 Watts 
Domain: DRAM 
Energy consumed: 1.46671 Joules 
Power consumed: 1.46671 Watts 
```