Known issues are always related to the latest stable release.
Please have also a look at the issue tracker about limitations and bugs.

  * The Intel Nehalem / Westmere Flop events are executed events. This causes that on all Nehalem processors the flop events overcount by about 5%
  * The Intel SandyBridge / IvyBridge Flop events are buggy. Do not trust them.
  * likwid-mpirun does not work right for hybrid OpenMPI/OpenMP