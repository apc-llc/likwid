﻿#summary Introduction to likwid
#labels Featured

# Motivation #

This is an effort to develop easy to use but yet powerful performance tools for
the GNU Linux operating system. While the focus of LIKWID is on x86 processors
some of the tools are portable and not limited to any specific architecture.
LIKWID follows the philosophy:

  * Simple
  * Efficient
  * Portable
  * Extensible


LIKWID includes the following tools:

  * [likwid-topology](LikwidTopology.md) : A tool to display the thread and cache topology on multicore/multisocket computers
  * [likwid-perfctr](LikwidPerfCtr.md) : A tool to measure hardware performance counters on recent Intel and AMD processors. It can be used as wrapper application without modifying the profiled code or with a marker API to measure only parts of the code.
  * [likwid-pin](LikwidPin.md) : A tool to pin your threaded application without changing your code. Works for pthreads and OpenMP.
  * [likwid-bench](LikwidBench.md) : Benchmarking framework allowing rapid prototyping of threaded assembly kernels
  * [likwid-mpirun](LikwidMpirun.md) : Script enabling simple and flexible pinning of MPI and MPI/threaded hybrid applications. With integrated likwid-perfctr support.
  * [likwid-powermeter](LikwidPowermeter.md) : Tool for accessing RAPL counters and query Turbo mode steps on Intel processor. RAPL counters are also available in likwid-perfctr.
  * [likwid-memsweeper](LikwidMemsweeper.md) : Tool to cleanup ccNUMA domains.
  * [likwid-features](LikwidFeatures.md) : A tool to toggle the prefetchers on Core 2 processors.

There was a BOF session on LIKWID at the ISC 13 conference. You can find the slides [here](http://wiki.likwid.googlecode.com/hg/BOF-slides.pdf) .

Papers you may find useful while using LIKWID:

  * [Best practices for HPM-assisted performance engineering on modern multicore processors](http://arxiv.org/pdf/1206.3738.pdf)
  * [LIKWID: Lightweight Performance Tools](http://arxiv.org/pdf/1104.4874.pdf)
  * [LIKWID: A lightweight performance-oriented tool suite for x86 multicore environments](http://arxiv.org/pdf/1004.4431.pdf)


A demo for a root exploit involving the msr device files was published. As a consequence the security settings for access to the msr device files are tightened in recent kernels.

Just setting the file access rights or using suid root on the access daemon is not sufficient anymore. You have to register your binary now to get access.

This is done by calling

`sudo setcap cap_sys_rawio+ep EXECUTABLE`

on the executables. This is only possible on local file systems.

# Wiki Overview #

  * How to [Build](Build.md) and install LIKWID.
  * KnownIssues for latest stable release
  * Be involved in the development of likwid on the [Ideapad](Ideapad.md).
  * Planning of upcoming releases on the ProjectPad.

# Acknowledgment #

If you use likwid for scientific work you can cite us as:

J. Treibig, G. Hager and G. Wellein: LIKWID: A lightweight performance-oriented tool suite for x86 multicore environments. Proceedings of PSTI2010, the First International Workshop on Parallel Software Tools and Tool Infrastructures, San Diego CA, September 13, 2010. DOI: 10.1109/ICPPW.2010.38 Preprint: http://arxiv.org/abs/1004.4431

Bibtex:
```
@inproceedings{psti,
 author               = {Treibig, J. and Hager, G. and Wellein, G.},
 booktitle            = {Proceedings of PSTI2010, the First International Workshop on Parallel Software Tools and Tool Infrastructures},
 title                = {LIKWID: A lightweight performance-oriented tool suite for x86 multicore environments},
 year                 = {2010},
 address = {San Diego CA},
 }
```