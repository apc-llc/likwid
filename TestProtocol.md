# Building #

  1. Change config.mk
  1. Build with all supported compilers. Check for compiler warnings.
  1. make install
  1. make uninstall


# Applications #

## likwid-topology ##

  1. Call likwid-topology -h. Check all flags on correctness.
  1. Call likwid-topology with all flag variants.
  1. Test likwid-topology on:
    * Intel Core 2
    * Intel Nehalem EP (with and without SMT)
    * Intel Nehalem EX
    * AMD K8
    * AMD K10

## likwid-pin ##

  1. Call likwid-pin -h. Check all flags on correctness.
  1. Call likwid-pin with all flag variants.
  1. Pin serial stream benchmark to process.
  1. Pin threaded OpenMP stream benchmark to Sockets on NUMA machine (gcc, icc, skip mask). Check for scaling bandwidth.

## likwid-features ##


## likwid-perfCtr ##

  1. Call likwid-perfCtr -h. Check all flags on correctness.
  1. Call likwid-perfCtr with all flag variants.
  1. Check all Performance groups on plausibility with likwid-bench on
    * Intel Core 2
    * Intel Nehalem EP
    * AMD K8
    * AMD K10
> Cases:
  1. Serial
  1. Threaded
  1. Marker (one call)
  1. Marker (accumulate)
  1. Custom events
  1. Uncore Events: Wrapper, API, Accumulated

## Formal issues ##

  1. Check file headers with date
  1. Check formatting
  1. Verify Version strings