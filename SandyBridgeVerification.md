# Hardware description #
Sockets: 2<br>
Cores per socket: 8<br>
Threads per core: 2<br>
Total number of processing units: 32<br>

<h1>Available groups</h1>
Each architecture defines a different set of groups. Here all the groups available for the Intel Core SandyBridge EP processor are listed:<br>
FLOPS_AVX: Packed AVX MFlops/s<br>
CLOCK: Power and Energy consumption<br>
MEM: Main memory bandwidth in MBytes/s<br>
MEM_DP: Overview of arithmetic and main memory performance<br>
ENERGY: Power and Energy consumption<br>
FLOPS_SP: Single Precision MFlops/s<br>
MEM_SP: Overview of arithmetic and main memory performance<br>
TLB: TLB miss rate/ratio<br>
L2: L2 cache bandwidth in MBytes/s<br>
L3: L3 cache bandwidth in MBytes/s<br>
BRANCH: Branch prediction miss rate/ratio<br>
L2CACHE: L2 cache miss rate/ratio<br>
FLOPS_DP: Double Precision MFlops/s<br>
DATA: Load to store ratio<br>

<h1>Available verification tests</h1>
Not all groups can be tested for accuracy. Here only the groups are listed that can be verified. Each group is followed by the low-level benchmarks that are performed for comparison. The benchmarks with <i>mem use non-temporal stores.</i><br>
MEM: load, store, copy, stream, triad, update, copy_mem, store_mem, stream_mem, triad_mem<br>
FLOPS_DP: stream, triad<br>
L2: load, store, copy, stream, triad, update<br>
FLOPS_AVX: sum_avx<br>
L3: load, store, copy, stream, triad, update<br>

<h1>Accuracy comparison</h1>
For each varification group, the tests are performed twice. Once in a plain manner without measuring but calculating the resulting values and once through an instumented code with LIKWID.<br>
<h2>Verification of Group MEM</h2>
<h3>Verification of Group MEM with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 70941       </td><td> 14           </td><td> 71819       </td><td> 19           </td><td> 71452.20    </td><td> 17.80        </td></tr>
<tr><td> 128kB   </td><td> 41038       </td><td> 14           </td><td> 43117       </td><td> 20           </td><td> 42558.70    </td><td> 15.20        </td></tr>
<tr><td> 2MB     </td><td> 26749       </td><td> 13           </td><td> 26769       </td><td> 16           </td><td> 26758.30    </td><td> 14.00        </td></tr>
<tr><td> 1GB     </td><td> 13369       </td><td> 13399        </td><td> 13387       </td><td> 13412        </td><td> 13378.00    </td><td> 13406.70     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 48473       </td><td> 14           </td><td> 48696       </td><td> 19           </td><td> 48603.50    </td><td> 17.00        </td></tr>
<tr><td> 128kB   </td><td> 28244       </td><td> 14           </td><td> 29329       </td><td> 15           </td><td> 28849.80    </td><td> 14.40        </td></tr>
<tr><td> 2MB     </td><td> 21190       </td><td> 13           </td><td> 21203       </td><td> 16           </td><td> 21194.50    </td><td> 14.00        </td></tr>
<tr><td> 1GB     </td><td> 10206       </td><td> 20472        </td><td> 10230       </td><td> 20484        </td><td> 10216.00    </td><td> 20479.40     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 95096       </td><td> 14           </td><td> 95544       </td><td> 19           </td><td> 95280.50    </td><td> 15.00        </td></tr>
<tr><td> 128kB   </td><td> 42966       </td><td> 14           </td><td> 46788       </td><td> 16           </td><td> 45635.80    </td><td> 14.20        </td></tr>
<tr><td> 2MB     </td><td> 26529       </td><td> 13           </td><td> 26563       </td><td> 15           </td><td> 26546.40    </td><td> 13.60        </td></tr>
<tr><td> 1GB     </td><td> 12479       </td><td> 18700        </td><td> 12484       </td><td> 18718        </td><td> 12481.10    </td><td> 18710.60     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 81126       </td><td> 14           </td><td> 82313       </td><td> 20           </td><td> 81633.00    </td><td> 17.20        </td></tr>
<tr><td> 128kB   </td><td> 45464       </td><td> 14           </td><td> 50372       </td><td> 15           </td><td> 49170.10    </td><td> 14.40        </td></tr>
<tr><td> 2MB     </td><td> 28294       </td><td> 13           </td><td> 28430       </td><td> 14           </td><td> 28389.70    </td><td> 13.70        </td></tr>
<tr><td> 1GB     </td><td> 13462       </td><td> 17971        </td><td> 13497       </td><td> 18003        </td><td> 13475.40    </td><td> 17988.89     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 94339       </td><td> 14           </td><td> 95139       </td><td> 22           </td><td> 94927.60    </td><td> 16.70        </td></tr>
<tr><td> 128kB   </td><td> 44993       </td><td> 14           </td><td> 47328       </td><td> 16           </td><td> 46497.50    </td><td> 14.90        </td></tr>
<tr><td> 2MB     </td><td> 28851       </td><td> 13           </td><td> 28876       </td><td> 15           </td><td> 28864.30    </td><td> 14.00        </td></tr>
<tr><td> 1GB     </td><td> 14007       </td><td> 17519        </td><td> 14035       </td><td> 17527        </td><td> 14020.80    </td><td> 17523.20     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 96721       </td><td> 14           </td><td> 97068       </td><td> 19           </td><td> 96948.80    </td><td> 15.10        </td></tr>
<tr><td> 128kB   </td><td> 54079       </td><td> 13           </td><td> 58370       </td><td> 14           </td><td> 57156.40    </td><td> 13.70        </td></tr>
<tr><td> 2MB     </td><td> 37361       </td><td> 13           </td><td> 37393       </td><td> 15           </td><td> 37380.00    </td><td> 13.50        </td></tr>
<tr><td> 1GB     </td><td> 21315       </td><td> 21354        </td><td> 21337       </td><td> 21365        </td><td> 21323.10    </td><td> 21361.00     </td></tr></tbody></table>

<h3>Verification of Group MEM with Test copy_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_copy_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 11579       </td><td> 4647         </td><td> 11644       </td><td> 5835         </td><td> 11632.50    </td><td> 5712.50      </td></tr>
<tr><td> 128kB   </td><td> 8339        </td><td> 4515         </td><td> 8380        </td><td> 4652         </td><td> 8370.50     </td><td> 4637.10      </td></tr>
<tr><td> 2MB     </td><td> 8100        </td><td> 4515         </td><td> 8103        </td><td> 8016         </td><td> 8101.80     </td><td> 4865.90      </td></tr>
<tr><td> 1GB     </td><td> 7564        </td><td> 8012         </td><td> 7572        </td><td> 8029         </td><td> 7568.80     </td><td> 8024.89      </td></tr></tbody></table>

<h3>Verification of Group MEM with Test triad_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_triad_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 17486       </td><td> 5823         </td><td> 17553       </td><td> 5994         </td><td> 17522.70    </td><td> 5849.60      </td></tr>
<tr><td> 128kB   </td><td> 14477       </td><td> 4045         </td><td> 14501       </td><td> 4092         </td><td> 14489.50    </td><td> 4084.90      </td></tr>
<tr><td> 2MB     </td><td> 13707       </td><td> 3882         </td><td> 13715       </td><td> 3884         </td><td> 13710.60    </td><td> 3882.90      </td></tr>
<tr><td> 1GB     </td><td> 11592       </td><td> 11967        </td><td> 11618       </td><td> 11982        </td><td> 11603.50    </td><td> 11974.20     </td></tr></tbody></table>

<h3>Verification of Group MEM with Test stream_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_stream_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 17426       </td><td> 5830         </td><td> 17473       </td><td> 5839         </td><td> 17455.30    </td><td> 5835.40      </td></tr>
<tr><td> 128kB   </td><td> 11048       </td><td> 4385         </td><td> 11210       </td><td> 4390         </td><td> 11188.30    </td><td> 4387.50      </td></tr>
<tr><td> 2MB     </td><td> 11110       </td><td> 4150         </td><td> 11134       </td><td> 4159         </td><td> 11123.20    </td><td> 4155.40      </td></tr>
<tr><td> 1GB     </td><td> 10070       </td><td> 10523        </td><td> 10086       </td><td> 10531        </td><td> 10079.50    </td><td> 10525.30     </td></tr></tbody></table>

<h3>Verification of Group MEM with Test store_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/MEM_store_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 5803        </td><td> 5828         </td><td> 5823        </td><td> 5838         </td><td> 5815.80     </td><td> 5834.40      </td></tr>
<tr><td> 128kB   </td><td> 5815        </td><td> 5828         </td><td> 5823        </td><td> 5837         </td><td> 5819.20     </td><td> 5834.00      </td></tr>
<tr><td> 2MB     </td><td> 5820        </td><td> 5834         </td><td> 5821        </td><td> 5836         </td><td> 5820.60     </td><td> 5835.00      </td></tr>
<tr><td> 1GB     </td><td> 5816        </td><td> 5837         </td><td> 5823        </td><td> 5838         </td><td> 5821.70     </td><td> 5837.90      </td></tr></tbody></table>


<h2>Verification of Group FLOPS_DP</h2>
<h3>Verification of Group FLOPS_DP with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/FLOPS_DP_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 6403        </td><td> 6497         </td><td> 6544        </td><td> 6669         </td><td> 6455.50     </td><td> 6633.60      </td></tr>
<tr><td> 24kB    </td><td> 6759        </td><td> 6772         </td><td> 6817        </td><td> 6846         </td><td> 6787.20     </td><td> 6811.90      </td></tr>
<tr><td> 128kB   </td><td> 3972        </td><td> 5349         </td><td> 4228        </td><td> 5418         </td><td> 4149.10     </td><td> 5382.70      </td></tr>
<tr><td> 2MB     </td><td> 2360        </td><td> 3991         </td><td> 2368        </td><td> 3998         </td><td> 2365.40     </td><td> 3994.20      </td></tr>
<tr><td> 1GB     </td><td> 1121        </td><td> 2214         </td><td> 1124        </td><td> 2226         </td><td> 1122.40     </td><td> 2219.50      </td></tr></tbody></table>


<h3>Verification of Group FLOPS_DP with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/FLOPS_DP_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 5633        </td><td> 5713         </td><td> 5747        </td><td> 5749         </td><td> 5694.80     </td><td> 5733.70      </td></tr>
<tr><td> 24kB    </td><td> 5921        </td><td> 5916         </td><td> 5952        </td><td> 5942         </td><td> 5928.70     </td><td> 5924.10      </td></tr>
<tr><td> 128kB   </td><td> 2876        </td><td> 3560         </td><td> 2960        </td><td> 3909         </td><td> 2912.20     </td><td> 3709.50      </td></tr>
<tr><td> 2MB     </td><td> 1803        </td><td> 2048         </td><td> 1804        </td><td> 2057         </td><td> 1803.40     </td><td> 2052.10      </td></tr>
<tr><td> 1GB     </td><td> 875         </td><td> 1208         </td><td> 877         </td><td> 1210         </td><td> 875.90      </td><td> 1208.40      </td></tr></tbody></table>


<h2>Verification of Group L2</h2>
<h3>Verification of Group L2 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 65388       </td><td> 7            </td><td> 67370       </td><td> 10           </td><td> 66126.80    </td><td> 7.60         </td></tr>
<tr><td> 1MB     </td><td> 26744       </td><td> 26757        </td><td> 26764       </td><td> 26781        </td><td> 26755.40    </td><td> 26768.80     </td></tr>
<tr><td> 4MB     </td><td> 26750       </td><td> 26768        </td><td> 26767       </td><td> 26782        </td><td> 26759.80    </td><td> 26773.20     </td></tr>
<tr><td> 1GB     </td><td> 13372       </td><td> 13371        </td><td> 13384       </td><td> 13388        </td><td> 13378.40    </td><td> 13380.60     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 46053       </td><td> 6            </td><td> 48091       </td><td> 7            </td><td> 47538.00    </td><td> 6.20         </td></tr>
<tr><td> 1MB     </td><td> 21192       </td><td> 42404        </td><td> 21217       </td><td> 42429        </td><td> 21204.80    </td><td> 42417.20     </td></tr>
<tr><td> 4MB     </td><td> 21218       </td><td> 42432        </td><td> 21225       </td><td> 42442        </td><td> 21221.20    </td><td> 42436.80     </td></tr>
<tr><td> 1GB     </td><td> 10209       </td><td> 20450        </td><td> 10237       </td><td> 20458        </td><td> 10221.60    </td><td> 20453.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 91663       </td><td> 10           </td><td> 92505       </td><td> 13           </td><td> 92049.40    </td><td> 11.40        </td></tr>
<tr><td> 1MB     </td><td> 26545       </td><td> 39802        </td><td> 26560       </td><td> 39857        </td><td> 26550.40    </td><td> 39839.00     </td></tr>
<tr><td> 4MB     </td><td> 26369       </td><td> 39617        </td><td> 26399       </td><td> 39653        </td><td> 26386.60    </td><td> 39634.40     </td></tr>
<tr><td> 1GB     </td><td> 12476       </td><td> 18720        </td><td> 12495       </td><td> 18727        </td><td> 12484.60    </td><td> 18722.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 77581       </td><td> 8            </td><td> 78299       </td><td> 11           </td><td> 77863.60    </td><td> 9.80         </td></tr>
<tr><td> 1MB     </td><td> 28470       </td><td> 37992        </td><td> 28508       </td><td> 38048        </td><td> 28491.60    </td><td> 38016.60     </td></tr>
<tr><td> 4MB     </td><td> 28204       </td><td> 37704        </td><td> 28263       </td><td> 37788        </td><td> 28242.80    </td><td> 37745.00     </td></tr>
<tr><td> 1GB     </td><td> 13458       </td><td> 17975        </td><td> 13491       </td><td> 17982        </td><td> 13478.20    </td><td> 17978.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 90970       </td><td> 9            </td><td> 91541       </td><td> 11           </td><td> 91318.00    </td><td> 10.40        </td></tr>
<tr><td> 1MB     </td><td> 28854       </td><td> 36183        </td><td> 28881       </td><td> 36217        </td><td> 28870.80    </td><td> 36198.00     </td></tr>
<tr><td> 4MB     </td><td> 28585       </td><td> 35898        </td><td> 28614       </td><td> 35910        </td><td> 28597.20    </td><td> 35903.80     </td></tr>
<tr><td> 1GB     </td><td> 13637       </td><td> 17515        </td><td> 14020       </td><td> 17522        </td><td> 13936.40    </td><td> 17518.40     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L2_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 94756       </td><td> 5            </td><td> 95178       </td><td> 7            </td><td> 94951.40    </td><td> 6.00         </td></tr>
<tr><td> 1MB     </td><td> 37413       </td><td> 37411        </td><td> 37455       </td><td> 37437        </td><td> 37441.20    </td><td> 37425.80     </td></tr>
<tr><td> 4MB     </td><td> 37424       </td><td> 37408        </td><td> 37433       </td><td> 37416        </td><td> 37428.60    </td><td> 37412.00     </td></tr>
<tr><td> 1GB     </td><td> 21291       </td><td> 21318        </td><td> 21332       </td><td> 21332        </td><td> 21318.40    </td><td> 21325.00     </td></tr></tbody></table>


<h2>Verification of Group FLOPS_AVX</h2>
<h3>Verification of Group FLOPS_AVX with Test sum_avx</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/FLOPS_AVX_sum_avx.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 23935       </td><td> 24017        </td><td> 24090       </td><td> 24105        </td><td> 24017.52    </td><td> 24078.06     </td></tr>
<tr><td> 128kB   </td><td> 8834        </td><td> 10451        </td><td> 8930        </td><td> 10610        </td><td> 8890.99     </td><td> 10564.20     </td></tr>
<tr><td> 2MB     </td><td> 6798        </td><td> 8035         </td><td> 6812        </td><td> 8046         </td><td> 6808.80     </td><td> 8040.68      </td></tr>
<tr><td> 1GB     </td><td> 3341        </td><td> 3740         </td><td> 3348        </td><td> 3742         </td><td> 3345.41     </td><td> 3741.46      </td></tr></tbody></table>


<h2>Verification of Group L3</h2>
<h3>Verification of Group L3 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 65261       </td><td> 3            </td><td> 67888       </td><td> 4            </td><td> 66396.60    </td><td> 3.80         </td></tr>
<tr><td> 1MB     </td><td> 26744       </td><td> 21823        </td><td> 26768       </td><td> 21841        </td><td> 26756.80    </td><td> 21836.80     </td></tr>
<tr><td> 4MB     </td><td> 26759       </td><td> 21864        </td><td> 26765       </td><td> 21875        </td><td> 26761.00    </td><td> 21871.60     </td></tr>
<tr><td> 1GB     </td><td> 13377       </td><td> 11296        </td><td> 13388       </td><td> 11304        </td><td> 13383.20    </td><td> 11301.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 47815       </td><td> 2            </td><td> 47949       </td><td> 4            </td><td> 47881.40    </td><td> 3.00         </td></tr>
<tr><td> 1MB     </td><td> 21199       </td><td> 33305        </td><td> 21209       </td><td> 33381        </td><td> 21203.00    </td><td> 33335.60     </td></tr>
<tr><td> 4MB     </td><td> 21212       </td><td> 33134        </td><td> 21230       </td><td> 33187        </td><td> 21222.40    </td><td> 33160.20     </td></tr>
<tr><td> 1GB     </td><td> 10204       </td><td> 17449        </td><td> 10240       </td><td> 17456        </td><td> 10226.20    </td><td> 17452.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 91508       </td><td> 5            </td><td> 92869       </td><td> 6            </td><td> 92258.40    </td><td> 5.80         </td></tr>
<tr><td> 1MB     </td><td> 26528       </td><td> 34794        </td><td> 26567       </td><td> 34891        </td><td> 26548.40    </td><td> 34860.20     </td></tr>
<tr><td> 4MB     </td><td> 26396       </td><td> 34709        </td><td> 26402       </td><td> 34874        </td><td> 26399.80    </td><td> 34749.40     </td></tr>
<tr><td> 1GB     </td><td> 12471       </td><td> 16889        </td><td> 12493       </td><td> 16893        </td><td> 12481.20    </td><td> 16891.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 77180       </td><td> 5            </td><td> 79232       </td><td> 5            </td><td> 78037.00    </td><td> 5.00         </td></tr>
<tr><td> 1MB     </td><td> 28479       </td><td> 34430        </td><td> 28509       </td><td> 34526        </td><td> 28501.00    </td><td> 34494.20     </td></tr>
<tr><td> 4MB     </td><td> 28239       </td><td> 34119        </td><td> 28262       </td><td> 34232        </td><td> 28249.00    </td><td> 34165.80     </td></tr>
<tr><td> 1GB     </td><td> 13463       </td><td> 16831        </td><td> 13491       </td><td> 16864        </td><td> 13474.80    </td><td> 16853.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 91185       </td><td> 6            </td><td> 91961       </td><td> 7            </td><td> 91579.80    </td><td> 6.20         </td></tr>
<tr><td> 1MB     </td><td> 28848       </td><td> 32541        </td><td> 28909       </td><td> 32607        </td><td> 28874.20    </td><td> 32561.00     </td></tr>
<tr><td> 4MB     </td><td> 28593       </td><td> 32177        </td><td> 28611       </td><td> 32192        </td><td> 28600.00    </td><td> 32188.20     </td></tr>
<tr><td> 1GB     </td><td> 14004       </td><td> 16283        </td><td> 14025       </td><td> 16291        </td><td> 14014.80    </td><td> 16286.20     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/sandyep1/L3_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 94959       </td><td> 3            </td><td> 95214       </td><td> 3            </td><td> 95078.20    </td><td> 3.00         </td></tr>
<tr><td> 1MB     </td><td> 37418       </td><td> 29949        </td><td> 37453       </td><td> 29980        </td><td> 37433.00    </td><td> 29966.20     </td></tr>
<tr><td> 4MB     </td><td> 37402       </td><td> 29865        </td><td> 37431       </td><td> 29884        </td><td> 37415.00    </td><td> 29878.60     </td></tr>
<tr><td> 1GB     </td><td> 21324       </td><td> 17077        </td><td> 21335       </td><td> 17090        </td><td> 21329.00    </td><td> 17082.80     </td></tr></tbody></table>

