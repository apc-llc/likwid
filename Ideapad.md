## Assembler code analyzer ##

It is helpful to be able to analyze the instructions used in a assembler code.
This means the instruction types (vectorized/ float / integer) and the
instruction count. Other useful information is the loop structure and the size
of a loop body instruction code. This would be especially helpful if combined
with a profiling run in order to focus on the hot loops.

## Performance Top ##

Implement a performance top based on likwid-perfctr. This can be as top but
with all relevant performance parameters for all cores.

## Using automatic instrumentation ##

Use automatic instrumentation to gain a quick overview about runtime distribution, call
chains and performance properties.
