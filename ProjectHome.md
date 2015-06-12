**NEWS** (last update 4.11.2014):<br>

There is a new bug fix release 3.1.3 available now.<br>
<br>
<a href='http://code.google.com/p/likwid/wiki/Changelog'>Changelog</a>:<br>
<br>
<ul><li>Full Uncore Support for Nehalem EX and Westmere EX<br>
</li><li>Atom Silvermont (Avoton + BayTrail) support<br>
</li><li>Read Marker API results and derived metrics in instrumented application (Patch by Julian Kunkel)<br>
</li><li>More low-level benchmarks for likwid-bench<br>
</li><li>Kernel module for enabling the RDPMC instruction<br>
</li><li>Use RDPMC for fixed and general purpose core-local counters if possible<br>
</li><li>New undocumented but working events<br>
</li><li>Support for all RAPL domains in likwid-powermeter<br>
</li><li>Better PCI device lookup<br>
</li><li>Lots of bug fixes</li></ul>

The release is available <a href='http://ftp.fau.de/pub/likwid/'>here</a>. This link is also available in the sidebar under Downloads.<br>
<br>
I will regularly blog posts about my likwid development and issues around performance related questions. You can find the blog here:<br>
<br>
<a href='http://likwid-tools.blogspot.com/'>http://likwid-tools.blogspot.com/</a>

<hr />

Likwid stands for <i>Like I knew what I am doing</i>. This project contributes easy to use command line tools for Linux to support programmers in developing high performance multi threaded programs.<br>
<br>
It contains the following tools:<br>
<ul><li><a href='http://code.google.com/p/likwid/wiki/LikwidTopology'>likwid-topology</a>: Show the thread and cache topology<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidPerfCtr'>likwid-perfctr</a>: Measure hardware performance counters on Intel and AMD processors<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidFeatures'>likwid-features</a>: Show and Toggle hardware prefetch control bits on Intel Core 2 processors<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidPin'>likwid-pin</a>: Pin your threaded application without touching your code (supports pthreads, Intel OpenMP and gcc OpenMP)<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidBench'>likwid-bench</a>: Benchmarking framework allowing rapid prototyping of threaded assembly kernels<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidMpirun'>likwid-mpirun</a>: Script enabling simple and flexible pinning of MPI and MPI/threaded hybrid applications<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidPerfscope'>likwid-perfscope</a>: Frontend for likwid-perfctr timeline mode. Allows live plotting of performance metrics.<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidPowermeter'>likwid-powermeter</a>: Tool for accessing RAPL counters and query Turbo mode steps on Intel processor.<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidMemsweeper'>likwid-memsweeper</a>: Tool to cleanup ccNUMA memory domains and force eviction of dirty cachelines from caches.<br>
</li><li><a href='http://code.google.com/p/likwid/wiki/LikwidSetFrequencies'>likwid-setFrequencies</a>: Tool to set specific processor frequencies.</li></ul>

Likwid stands out because:<br>
<br>
<ul><li><b>No kernel patching</b>, any vanilla linux 2.6 or newer kernel works<br>
</li><li><b>Transparent</b>, always clear which events are chosen,  event tags have the same naming as in documentation<br>
</li><li><b>Lightweight</b>, LIKWID tries to add no overhead and keeps out of your way.<br>
</li><li><b>Easy to use</b>,  simple to build, no need to touch your code, configurable from outside. Clear CLI interface.<br>
</li><li><b>Multiplatform</b>, likwid supports Intel and AMD processors<br>
</li><li><b>Up to date</b>, likwid tries to fully support new processors as soon as possible<br>
</li><li><b>Extensible</b>, you can add functionality by means of simple text files</li></ul>

If you encounter problems feel free to ask questions in the <a href='http://groups.google.com/group/likwid-users'>User Mailing List</a>.<br>
<br>
<br>
