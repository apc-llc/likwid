# Introduction #

Intel Xeon Phi processors support the P6 HPM interface.

It has the following support for performance monitoring:

  * Two general purpose performance counter registers (40 bit wide)
  * Most events can be measured per SMT thread

If you want to use LIKWID on a Xeon Phi you have to use set MIC as COMPILER in config.mk.
This build of LIKWID will not be binary compatible with other X86 processors.
To use LIKWID you have to turn of power management on the MIC. LIKWID relies on
RDTSC being used for wallclock time. On the MIC this is only given if power
management is turned off. This can be configured in
/etc/sysconfig/mic/default.conf.

At the end of this file the power management is configured. The following
configuration worked:

```
    PowerManagement "cpufreq_off;corec6_off;pc3_off;pc6_off"
```


# Build #

To compile LIKWID for Phi set the following  in `config.mk`:

```
COMPILER = MIC#NO SPACE
BUILDDAEMON = false#NO SPACE
ACCESSMODE = direct#NO SPACE
```

Then build and install as usual.

# Performance groups #

For an exact documentation of the performance groups call likwid-perfctr with
the -g GROUP\_TAG -H switch. This will output a detailed documentation of the
performance group. Please note that because of the limited number of counters
on this architectures the groups are very limited. Future releases will add
multiplexing to allow for more meaningful performance groups.

Supported Groups:

You can find out about supported groups with likwid-perfctr -a.

CACHE: Compute to Data Access Ratio <br>
CPI: Cycles per instruction<br>
L2CACHE: L2 Compute to Data Access Ratio<br>
MEM1: L2 Write Misses<br>
MEM2: L2 Read Misses<br>
MEM3: HW prefetch transfers<br>
MEM4: L2 Victim requests<br>
MEM5: L2 Snoop hits<br>
MEM6: L2 Read Misses<br>
PAIRING: Pairing ratio<br>
READ_MISS_RATIO: Miss ratio for data read<br>
WRITE_MISS_RATIO: Miss ratio for data write<br>
VECTOR: Vector unit usage<br>
VECTOR2: Vector unit usage<br>
VPU_FILL_RATIO_DBL: VPU filling for double<br>
VPU_PAIRING: VPU Pairing ratio<br>
VPU_READ_MISS_RATIO: Miss ratio for VPU data read<br>
VPU_WRITE_MISS_RATIO: Miss ratio for VPU data write<br>


<h1>Counters</h1>

2 General Purpose Counters: PMC0, PMC1.<br>
<br>
<h1>Events</h1>

This architecture has 61 events.<br>
For a recent list of supported events execute likwid-perfctr with the -e switch.