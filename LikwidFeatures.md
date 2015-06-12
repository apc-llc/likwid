﻿#summary likwid-features: Tool to read out and toggle the hardware prefetcher state on Intel Core 2 processors



# Introduction #

Modern processors have various hardware prefetchers to hide data access latencies for deterministic data access patterns. On Intel processors there exists the possibility to turn these prefetchers on and off. This is realized by setting bits in the MSR\_IA32\_MISC\_ENABLE MSR. likwid-features allows to view and toggle the flags in this MSR in an easy way.

This is only tested on Intel Core 2 processors. It is not clear if it also works on Intel i7 processors.

# Usage #

As usual you can get a short help message with
```
 likwid-features -h
```


# Options #

# Example #
