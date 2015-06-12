# Hardware description #
Sockets: 2<br>
Cores per socket: 10<br>
Threads per core: 2<br>
Total number of processing units: 40<br>

<h1>Available groups</h1>
Each architecture defines a different set of groups. Here all the groups available for the Intel Core IvyBridge EP processor are listed:<br>
FLOPS_AVX: Packed AVX MFlops/s<br>
CLOCK: Power and Energy consumption<br>
MEM: Main memory bandwidth in MBytes/s<br>
MEM_DP: Power and Energy consumption<br>
ENERGY: Power and Energy consumption<br>
FLOPS_SP: Single Precision MFlops/s<br>
MEM_SP: Power and Energy consumption<br>
TLB: TLB miss rate/ratio<br>
L2: L2 cache bandwidth in MBytes/s<br>
L3: L3 cache bandwidth in MBytes/s<br>
BRANCH: Branch prediction miss rate/ratio<br>
L2CACHE: L2 cache miss rate/ratio<br>
FLOPS_DP: Double Precision MFlops/s<br>
DATA: Load to store ratio<br>

<h1>Group to events relation</h1>
Events of group MEM:<br>
CAS_COUNT_RD<br>
CAS_COUNT_WR<br>
Calculate Memory Bandwidth (MByte/s): ((sum(CAS_COUNT_RD,MBOX<code>*</code>) + sum(CAS_COUNT_WR,MBOX<code>*</code>)) <code>*</code> CACHELINE_SIZE) / (MEASUREMENT_TIME <code>*</code> 1.0E6)<br>
<br>
Events of group FLOPS_DP:<br>
FP_COMP_OPS_EXE_SSE_FP_PACKED_DOUBLE<br>
FP_COMP_OPS_EXE_SSE_FP_SCALAR_DOUBLE<br>
SIMD_FP_256_PACKED_DOUBLE<br>
Calculate MFLOP/s: (FP_COMP_OPS_EXE_SSE_FP_SCALAR_DOUBLE + (2 <code>*</code> FP_COMP_OPS_EXE_SSE_FP_PACKED_DOUBLE) + (4 <code>*</code> SIMD_FP_256_PACKED_DOUBLE)) / (MEASUREMENT_TIME <code>*</code> 1.0E6)<br>
<br>
Events of group L2:<br>
L1D_REPLACEMENT<br>
L1D_M_EVICT<br>
Calculate L2 Bandwidth: ((L1D_REPLACEMENT + L1D_M_EVICT) <code>*</code> CACHELINE_SIZE) / (MEASUREMENT_TIME <code>*</code> 1.0E6)<br>
<br>
Events of group FLOPS_SP:<br>
FP_COMP_OPS_EXE_SSE_FP_PACKED_SINGLE<br>
FP_COMP_OPS_EXE_SSE_FP_SCALAR_SINGLE<br>
SIMD_FP_256_PACKED_SINGLE<br>
Calculate MFLOP/s: (FP_COMP_OPS_EXE_SSE_FP_SCALAR_SINGLE + (2 <code>*</code> FP_COMP_OPS_EXE_SSE_FP_PACKED_SINGLE) + (4 <code>*</code> SIMD_FP_256_PACKED_SINGLE)) / (MEASUREMENT_TIME <code>*</code> 1.0E6)<br>
<br>
Events of group L3:<br>
L2_LINES_IN_ALL<br>
L2_LINES_OUT_DIRTY_ALL<br>
Calculate L3 Bandwidth: ((L2_LINES_IN_ALL + L2_LINES_OUT_DIRTY_ALL) <code>*</code> CACHELINE_SIZE) / (MEASUREMENT_TIME <code>*</code> 1.0E6)<br>

<h1>Available verification tests</h1>
Not all groups can be tested for accuracy. Here only the groups are listed that can be verified. Each group is followed by the low-level benchmarks that are performed for comparison.<br>
MEM: load, store, copy, stream, triad, update, copy_mem, triad_mem, stream_mem, store_mem<br>
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
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 68274       </td><td> 15           </td><td> 70537       </td><td> 19           </td><td> 69256.60    </td><td> 16.70        </td></tr>
<tr><td> 128kB   </td><td> 41218       </td><td> 15           </td><td> 42321       </td><td> 17           </td><td> 41881.20    </td><td> 16.10        </td></tr>
<tr><td> 2MB     </td><td> 27266       </td><td> 15           </td><td> 27304       </td><td> 16           </td><td> 27288.30    </td><td> 15.20        </td></tr>
<tr><td> 1GB     </td><td> 16243       </td><td> 16341        </td><td> 16427       </td><td> 16531        </td><td> 16305.60    </td><td> 16407.10     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 47124       </td><td> 17           </td><td> 47318       </td><td> 22           </td><td> 47222.50    </td><td> 19.60        </td></tr>
<tr><td> 128kB   </td><td> 29763       </td><td> 16           </td><td> 30662       </td><td> 28           </td><td> 30350.30    </td><td> 18.00        </td></tr>
<tr><td> 2MB     </td><td> 20581       </td><td> 15           </td><td> 20601       </td><td> 16           </td><td> 20593.20    </td><td> 15.40        </td></tr>
<tr><td> 1GB     </td><td> 9000        </td><td> 17657        </td><td> 9017        </td><td> 17686        </td><td> 9008.70     </td><td> 17670.60     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 92545       </td><td> 15           </td><td> 92954       </td><td> 20           </td><td> 92821.80    </td><td> 16.80        </td></tr>
<tr><td> 128kB   </td><td> 43313       </td><td> 15           </td><td> 45512       </td><td> 17           </td><td> 44734.30    </td><td> 15.80        </td></tr>
<tr><td> 2MB     </td><td> 25799       </td><td> 15           </td><td> 25831       </td><td> 17           </td><td> 25819.20    </td><td> 15.50        </td></tr>
<tr><td> 1GB     </td><td> 11737       </td><td> 17391        </td><td> 11764       </td><td> 17455        </td><td> 11748.90    </td><td> 17420.20     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 79211       </td><td> 15           </td><td> 79715       </td><td> 18           </td><td> 79414.40    </td><td> 16.00        </td></tr>
<tr><td> 128kB   </td><td> 44710       </td><td> 16           </td><td> 49559       </td><td> 19           </td><td> 48065.00    </td><td> 16.90        </td></tr>
<tr><td> 2MB     </td><td> 27607       </td><td> 15           </td><td> 27666       </td><td> 16           </td><td> 27647.70    </td><td> 15.60        </td></tr>
<tr><td> 1GB     </td><td> 12467       </td><td> 16515        </td><td> 12483       </td><td> 16538        </td><td> 12475.40    </td><td> 16530.10     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 88668       </td><td> 15           </td><td> 91267       </td><td> 27           </td><td> 89995.10    </td><td> 17.40        </td></tr>
<tr><td> 128kB   </td><td> 44071       </td><td> 15           </td><td> 45885       </td><td> 23           </td><td> 45210.80    </td><td> 16.70        </td></tr>
<tr><td> 2MB     </td><td> 27906       </td><td> 15           </td><td> 28184       </td><td> 22           </td><td> 28141.60    </td><td> 16.00        </td></tr>
<tr><td> 1GB     </td><td> 10889       </td><td> 13543        </td><td> 11653       </td><td> 13642        </td><td> 10985.40    </td><td> 13599.50     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 94128       </td><td> 15           </td><td> 94365       </td><td> 18           </td><td> 94259.90    </td><td> 16.70        </td></tr>
<tr><td> 128kB   </td><td> 54127       </td><td> 15           </td><td> 56991       </td><td> 21           </td><td> 55887.30    </td><td> 16.50        </td></tr>
<tr><td> 2MB     </td><td> 36630       </td><td> 15           </td><td> 36655       </td><td> 16           </td><td> 36642.80    </td><td> 15.30        </td></tr>
<tr><td> 1GB     </td><td> 19077       </td><td> 18701        </td><td> 19116       </td><td> 18734        </td><td> 19096.50    </td><td> 18719.30     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test copy_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_copy_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 11275       </td><td> 5637         </td><td> 11301       </td><td> 5668         </td><td> 11289.50    </td><td> 5662.30      </td></tr>
<tr><td> 128kB   </td><td> 8094        </td><td> 4491         </td><td> 8113        </td><td> 4512         </td><td> 8106.90     </td><td> 4506.10      </td></tr>
<tr><td> 2MB     </td><td> 7935        </td><td> 4427         </td><td> 7940        </td><td> 4428         </td><td> 7937.10     </td><td> 4427.80      </td></tr>
<tr><td> 1GB     </td><td> 7386        </td><td> 7765         </td><td> 7398        </td><td> 7783         </td><td> 7392.10     </td><td> 7771.20      </td></tr></tbody></table>


<h3>Verification of Group MEM with Test triad_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_triad_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 17400       </td><td> 5641         </td><td> 17582       </td><td> 5661         </td><td> 17488.50    </td><td> 5652.10      </td></tr>
<tr><td> 128kB   </td><td> 12579       </td><td> 3950         </td><td> 12668       </td><td> 3965         </td><td> 12649.80    </td><td> 3959.90      </td></tr>
<tr><td> 2MB     </td><td> 13466       </td><td> 3820         </td><td> 13477       </td><td> 3827         </td><td> 13471.20    </td><td> 3824.60      </td></tr>
<tr><td> 1GB     </td><td> 11396       </td><td> 11730        </td><td> 11428       </td><td> 11790        </td><td> 11415.00    </td><td> 11751.80     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test stream_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_stream_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 16931       </td><td> 5655         </td><td> 16957       </td><td> 5670         </td><td> 16945.60    </td><td> 5665.20      </td></tr>
<tr><td> 128kB   </td><td> 10148       </td><td> 4277         </td><td> 10179       </td><td> 4287         </td><td> 10160.00    </td><td> 4284.20      </td></tr>
<tr><td> 2MB     </td><td> 11048       </td><td> 4115         </td><td> 11061       </td><td> 4125         </td><td> 11054.50    </td><td> 4120.80      </td></tr>
<tr><td> 1GB     </td><td> 9898        </td><td> 10235        </td><td> 9915        </td><td> 10251        </td><td> 9903.10     </td><td> 10241.70     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test store_mem</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/MEM_store_mem.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 4892        </td><td> 5649         </td><td> 4907        </td><td> 5667         </td><td> 4900.40     </td><td> 5661.50      </td></tr>
<tr><td> 128kB   </td><td> 5642        </td><td> 5658         </td><td> 5648        </td><td> 5664         </td><td> 5646.20     </td><td> 5661.30      </td></tr>
<tr><td> 2MB     </td><td> 5641        </td><td> 5659         </td><td> 5644        </td><td> 5660         </td><td> 5643.40     </td><td> 5659.70      </td></tr>
<tr><td> 1GB     </td><td> 5632        </td><td> 5557         </td><td> 5634        </td><td> 5559         </td><td> 5633.00     </td><td> 5557.80      </td></tr></tbody></table>


<h2>Verification of Group FLOPS_DP</h2>
<h3>Verification of Group FLOPS_DP with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/FLOPS_DP_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 6354        </td><td> 6340         </td><td> 6456        </td><td> 6471         </td><td> 6399.70     </td><td> 6421.20      </td></tr>
<tr><td> 24kB    </td><td> 6608        </td><td> 6597         </td><td> 6654        </td><td> 6636         </td><td> 6625.30     </td><td> 6621.90      </td></tr>
<tr><td> 128kB   </td><td> 3997        </td><td> 5103         </td><td> 4137        </td><td> 5280         </td><td> 4091.80     </td><td> 5217.50      </td></tr>
<tr><td> 2MB     </td><td> 2090        </td><td> 3745         </td><td> 2307        </td><td> 3783         </td><td> 2282.40     </td><td> 3760.60      </td></tr>
<tr><td> 1GB     </td><td> 1041        </td><td> 1711         </td><td> 1043        </td><td> 1727         </td><td> 1041.80     </td><td> 1721.70      </td></tr></tbody></table>


<h3>Verification of Group FLOPS_DP with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/FLOPS_DP_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 5552        </td><td> 5563         </td><td> 5589        </td><td> 5588         </td><td> 5572.40     </td><td> 5578.50      </td></tr>
<tr><td> 24kB    </td><td> 5587        </td><td> 5661         </td><td> 5717        </td><td> 5725         </td><td> 5642.40     </td><td> 5688.00      </td></tr>
<tr><td> 128kB   </td><td> 2842        </td><td> 3474         </td><td> 2905        </td><td> 3890         </td><td> 2870.90     </td><td> 3696.60      </td></tr>
<tr><td> 2MB     </td><td> 1758        </td><td> 2002         </td><td> 1762        </td><td> 2054         </td><td> 1760.00     </td><td> 2009.00      </td></tr>
<tr><td> 1GB     </td><td> 679         </td><td> 903          </td><td> 683         </td><td> 915          </td><td> 681.60      </td><td> 909.20       </td></tr></tbody></table>


<h2>Verification of Group L2</h2>
<h3>Verification of Group L2 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 63300       </td><td> 6            </td><td> 66422       </td><td> 8            </td><td> 65332.80    </td><td> 6.80         </td></tr>
<tr><td> 1MB     </td><td> 27269       </td><td> 27292        </td><td> 27295       </td><td> 27351        </td><td> 27279.80    </td><td> 27322.60     </td></tr>
<tr><td> 4MB     </td><td> 27399       </td><td> 26579        </td><td> 27419       </td><td> 27472        </td><td> 27410.20    </td><td> 27292.00     </td></tr>
<tr><td> 1GB     </td><td> 16247       </td><td> 16279        </td><td> 16404       </td><td> 16357        </td><td> 16318.60    </td><td> 16333.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 46563       </td><td> 4            </td><td> 46625       </td><td> 6            </td><td> 46601.80    </td><td> 5.00         </td></tr>
<tr><td> 1MB     </td><td> 20613       </td><td> 20540        </td><td> 20624       </td><td> 20621        </td><td> 20619.00    </td><td> 20597.60     </td></tr>
<tr><td> 4MB     </td><td> 20490       </td><td> 20534        </td><td> 20501       </td><td> 20538        </td><td> 20498.20    </td><td> 20536.20     </td></tr>
<tr><td> 1GB     </td><td> 8980        </td><td> 8791         </td><td> 9000        </td><td> 8807         </td><td> 8990.60     </td><td> 8797.00      </td></tr></tbody></table>


<h3>Verification of Group L2 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 89549       </td><td> 8            </td><td> 90306       </td><td> 10           </td><td> 89765.40    </td><td> 8.60         </td></tr>
<tr><td> 1MB     </td><td> 25796       </td><td> 25809        </td><td> 25843       </td><td> 25854        </td><td> 25818.20    </td><td> 25826.40     </td></tr>
<tr><td> 4MB     </td><td> 25685       </td><td> 25732        </td><td> 25706       </td><td> 25755        </td><td> 25693.80    </td><td> 25745.40     </td></tr>
<tr><td> 1GB     </td><td> 11720       </td><td> 11566        </td><td> 11746       </td><td> 11594        </td><td> 11727.20    </td><td> 11581.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 76412       </td><td> 5            </td><td> 77378       </td><td> 8            </td><td> 76878.60    </td><td> 7.00         </td></tr>
<tr><td> 1MB     </td><td> 27668       </td><td> 27698        </td><td> 27701       </td><td> 27714        </td><td> 27688.40    </td><td> 27709.60     </td></tr>
<tr><td> 4MB     </td><td> 27408       </td><td> 27481        </td><td> 27499       </td><td> 27560        </td><td> 27456.80    </td><td> 27514.20     </td></tr>
<tr><td> 1GB     </td><td> 12501       </td><td> 12401        </td><td> 12514       </td><td> 12413        </td><td> 12506.60    </td><td> 12408.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 88937       </td><td> 8            </td><td> 89403       </td><td> 10           </td><td> 89103.80    </td><td> 8.80         </td></tr>
<tr><td> 1MB     </td><td> 28162       </td><td> 28287        </td><td> 28238       </td><td> 28320        </td><td> 28205.20    </td><td> 28300.60     </td></tr>
<tr><td> 4MB     </td><td> 27939       </td><td> 28084        </td><td> 27963       </td><td> 28117        </td><td> 27952.20    </td><td> 28104.00     </td></tr>
<tr><td> 1GB     </td><td> 10870       </td><td> 10839        </td><td> 10921       </td><td> 10885        </td><td> 10898.40    </td><td> 10868.60     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L2_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 89932       </td><td> 4            </td><td> 92852       </td><td> 5            </td><td> 92082.80    </td><td> 4.60         </td></tr>
<tr><td> 1MB     </td><td> 36446       </td><td> 18329        </td><td> 36692       </td><td> 18345        </td><td> 36625.60    </td><td> 18334.60     </td></tr>
<tr><td> 4MB     </td><td> 34893       </td><td> 18211        </td><td> 36376       </td><td> 18220        </td><td> 36077.00    </td><td> 18215.60     </td></tr>
<tr><td> 1GB     </td><td> 19047       </td><td> 9330         </td><td> 19070       </td><td> 9337         </td><td> 19058.80    </td><td> 9334.40      </td></tr></tbody></table>


<h2>Verification of Group FLOPS_AVX</h2>
<h3>Verification of Group FLOPS_AVX with Test sum_avx</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/FLOPS_AVX_sum_avx.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 23221       </td><td> 23170        </td><td> 23316       </td><td> 23305        </td><td> 23281.50    </td><td> 23269.54     </td></tr>
<tr><td> 128kB   </td><td> 8353        </td><td> 9798         </td><td> 8720        </td><td> 10404        </td><td> 8626.49     </td><td> 10281.72     </td></tr>
<tr><td> 2MB     </td><td> 6663        </td><td> 8079         </td><td> 6670        </td><td> 8092         </td><td> 6667.26     </td><td> 8086.89      </td></tr>
<tr><td> 1GB     </td><td> 3742        </td><td> 4112         </td><td> 3756        </td><td> 4126         </td><td> 3746.23     </td><td> 4115.26      </td></tr></tbody></table>

<h2>Verification of Group L3</h2>
<h3>Verification of Group L3 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 63288       </td><td> 3            </td><td> 67410       </td><td> 4            </td><td> 66208.80    </td><td> 3.80         </td></tr>
<tr><td> 1MB     </td><td> 27280       </td><td> 22707        </td><td> 27313       </td><td> 22730        </td><td> 27297.20    </td><td> 22720.60     </td></tr>
<tr><td> 4MB     </td><td> 27404       </td><td> 22989        </td><td> 27413       </td><td> 23018        </td><td> 27408.60    </td><td> 22997.20     </td></tr>
<tr><td> 1GB     </td><td> 16264       </td><td> 14509        </td><td> 16318       </td><td> 14529        </td><td> 16303.40    </td><td> 14520.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 45202       </td><td> 3            </td><td> 46648       </td><td> 3            </td><td> 46349.20    </td><td> 3.00         </td></tr>
<tr><td> 1MB     </td><td> 20601       </td><td> 32439        </td><td> 20623       </td><td> 32490        </td><td> 20613.00    </td><td> 32466.00     </td></tr>
<tr><td> 4MB     </td><td> 20493       </td><td> 32215        </td><td> 20506       </td><td> 32236        </td><td> 20502.20    </td><td> 32222.40     </td></tr>
<tr><td> 1GB     </td><td> 9003        </td><td> 15740        </td><td> 9020        </td><td> 15765        </td><td> 9012.60     </td><td> 15749.20     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 89594       </td><td> 6            </td><td> 90277       </td><td> 7            </td><td> 89947.20    </td><td> 6.20         </td></tr>
<tr><td> 1MB     </td><td> 25800       </td><td> 34084        </td><td> 25821       </td><td> 34122        </td><td> 25811.60    </td><td> 34103.40     </td></tr>
<tr><td> 4MB     </td><td> 25707       </td><td> 33975        </td><td> 25721       </td><td> 34013        </td><td> 25712.20    </td><td> 33993.20     </td></tr>
<tr><td> 1GB     </td><td> 11725       </td><td> 16181        </td><td> 11771       </td><td> 16231        </td><td> 11742.40    </td><td> 16204.00     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 76664       </td><td> 5            </td><td> 77189       </td><td> 6            </td><td> 76841.20    </td><td> 5.40         </td></tr>
<tr><td> 1MB     </td><td> 27682       </td><td> 33435        </td><td> 27703       </td><td> 33770        </td><td> 27691.80    </td><td> 33688.40     </td></tr>
<tr><td> 4MB     </td><td> 27414       </td><td> 33379        </td><td> 27501       </td><td> 33507        </td><td> 27473.40    </td><td> 33455.40     </td></tr>
<tr><td> 1GB     </td><td> 12503       </td><td> 15962        </td><td> 12524       </td><td> 15991        </td><td> 12516.80    </td><td> 15978.80     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 88739       </td><td> 6            </td><td> 89246       </td><td> 8            </td><td> 88943.00    </td><td> 6.60         </td></tr>
<tr><td> 1MB     </td><td> 28026       </td><td> 32071        </td><td> 28212       </td><td> 32157        </td><td> 28169.20    </td><td> 32103.60     </td></tr>
<tr><td> 4MB     </td><td> 27707       </td><td> 31782        </td><td> 27952       </td><td> 31856        </td><td> 27884.20    </td><td> 31815.20     </td></tr>
<tr><td> 1GB     </td><td> 10912       </td><td> 13364        </td><td> 10925       </td><td> 13389        </td><td> 10917.60    </td><td> 13379.60     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/ivyep1/L3_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 92566       </td><td> 3            </td><td> 92823       </td><td> 3            </td><td> 92717.80    </td><td> 3.00         </td></tr>
<tr><td> 1MB     </td><td> 36652       </td><td> 29744        </td><td> 36679       </td><td> 29777        </td><td> 36668.40    </td><td> 29757.00     </td></tr>
<tr><td> 4MB     </td><td> 36339       </td><td> 29071        </td><td> 36363       </td><td> 29084        </td><td> 36356.60    </td><td> 29078.20     </td></tr>
<tr><td> 1GB     </td><td> 19083       </td><td> 16817        </td><td> 19108       </td><td> 16828        </td><td> 19094.20    </td><td> 16823.20     </td></tr>