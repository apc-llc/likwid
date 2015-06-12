# Hardware description #
Sockets: 2<br>
Cores per socket: 6<br>
Threads per core: 2<br>
Total number of processing units: 24<br>

<h1>Available groups</h1>
Each architecture defines a different set of groups. Here all the groups available for the Intel Core Westmere processor are listed:<br>
MEM: Main memory bandwidth<br>
FLOPS_X87: X87 MFlops/s<br>
CACHE: Data cache miss rate/ratio<br>
FLOPS_SP: Single Precision MFlops/s<br>
L3CACHE: L3 cache miss rate/ratio<br>
TLB: TLB miss rate/ratio<br>
L2: L2 cache bandwidth in MBytes/s<br>
L3: L3 cache bandwidth in MBytes/s<br>
BRANCH: Branch prediction miss rate/ratio<br>
L2CACHE: L2 cache miss rate/ratio<br>
FLOPS_DP: Double Precision MFlops/s<br>
DATA: Load to store ratio<br>
VIEW: Overview of arithmetic and memory performance<br>

<h1>Available verification tests</h1>
Not all groups can be tested for accuracy. Here only the groups are listed that can be verified. Each group is followed by the low-level benchmarks that are performed for comparison.<br>
MEM: load, store, copy, stream, triad, update<br>
FLOPS_DP: stream, triad<br>
L2: load, store, copy, stream, triad, update<br>
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
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 36767       </td><td> 0            </td><td> 37016       </td><td> 0            </td><td> 36970       </td><td> 0            </td></tr>
<tr><td> 128kB   </td><td> 26074       </td><td> 0            </td><td> 26229       </td><td> 0            </td><td> 26161       </td><td> 0            </td></tr>
<tr><td> 2MB     </td><td> 21682       </td><td> 0            </td><td> 21759       </td><td> 0            </td><td> 21714       </td><td> 0            </td></tr>
<tr><td> 1GB     </td><td> 12612       </td><td> 12659        </td><td> 12618       </td><td> 12663        </td><td> 12615       </td><td> 12662        </td></tr></tbody></table>



<h3>Verification of Group MEM with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 45876       </td><td> 0            </td><td> 45948       </td><td> 1            </td><td> 45900.95    </td><td> 0.50         </td></tr>
<tr><td> 128kB   </td><td> 27821       </td><td> 0            </td><td> 28234       </td><td> 0            </td><td> 28032.41    </td><td> 0.33         </td></tr>
<tr><td> 2MB     </td><td> 17538       </td><td> 0            </td><td> 17547       </td><td> 0            </td><td> 17542.75    </td><td> 0.29         </td></tr>
<tr><td> 1GB     </td><td> 6718        </td><td> 13213        </td><td> 6738        </td><td> 13248        </td><td> 6727.33     </td><td> 13224.00     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 72382       </td><td> 0            </td><td> 72890       </td><td> 1            </td><td> 72740.38    </td><td> 0.55         </td></tr>
<tr><td> 128kB   </td><td> 34720       </td><td> 0            </td><td> 35610       </td><td> 1            </td><td> 35366.84    </td><td> 0.38         </td></tr>
<tr><td> 2MB     </td><td> 22836       </td><td> 0            </td><td> 22871       </td><td> 0            </td><td> 22857.34    </td><td> 0.29         </td></tr>
<tr><td> 1GB     </td><td> 8358        </td><td> 12417        </td><td> 8449        </td><td> 12485        </td><td> 8416.78     </td><td> 12460.88     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 67313       </td><td> 0            </td><td> 67725       </td><td> 1            </td><td> 67641.84    </td><td> 0.40         </td></tr>
<tr><td> 128kB   </td><td> 31181       </td><td> 0            </td><td> 32117       </td><td> 1            </td><td> 31844.30    </td><td> 0.41         </td></tr>
<tr><td> 2MB     </td><td> 22030       </td><td> 0            </td><td> 22052       </td><td> 0            </td><td> 22043.29    </td><td> 0.23         </td></tr>
<tr><td> 1GB     </td><td> 9013        </td><td> 11928        </td><td> 9074        </td><td> 12001        </td><td> 9044.80     </td><td> 11957.35     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 60157       </td><td> 0            </td><td> 60476       </td><td> 1            </td><td> 60430.22    </td><td> 0.53         </td></tr>
<tr><td> 128kB   </td><td> 31523       </td><td> 0            </td><td> 31710       </td><td> 0            </td><td> 31633.19    </td><td> 0.39         </td></tr>
<tr><td> 2MB     </td><td> 23533       </td><td> 0            </td><td> 23547       </td><td> 0            </td><td> 23541.83    </td><td> 0.31         </td></tr>
<tr><td> 1GB     </td><td> 9162        </td><td> 11331        </td><td> 9290        </td><td> 11448        </td><td> 9227.16     </td><td> 11411.51     </td></tr></tbody></table>


<h3>Verification of Group MEM with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 24kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/MEM_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 24kB    </td><td> 73668       </td><td> 0            </td><td> 73934       </td><td> 0            </td><td> 73879.77    </td><td> 0.27         </td></tr>
<tr><td> 128kB   </td><td> 44118       </td><td> 0            </td><td> 44622       </td><td> 0            </td><td> 44460.33    </td><td> 0.29         </td></tr>
<tr><td> 2MB     </td><td> 29306       </td><td> 0            </td><td> 29319       </td><td> 0            </td><td> 29313.46    </td><td> 0.27         </td></tr>
<tr><td> 1GB     </td><td> 13204       </td><td> 12993        </td><td> 13247       </td><td> 13043        </td><td> 13220.05    </td><td> 13014.25     </td></tr></tbody></table>

<h2>Verification of Group FLOPS_DP</h2>
<h3>Verification of Group FLOPS_DP with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/FLOPS_DP_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 5580        </td><td> 5590         </td><td> 5582        </td><td> 5663         </td><td> 5581        </td><td> 5646         </td></tr>
<tr><td> 24kB    </td><td> 5608        </td><td> 5638         </td><td> 5641        </td><td> 5677         </td><td> 5630        </td><td> 5671         </td></tr>
<tr><td> 128kB   </td><td> 2621        </td><td> 2833         </td><td> 2675        </td><td> 2899         </td><td> 2662        </td><td> 2887         </td></tr>
<tr><td> 2MB     </td><td> 1835        </td><td> 2087         </td><td> 1837        </td><td> 2092         </td><td> 1836        </td><td> 2090         </td></tr>
<tr><td> 1GB     </td><td> 748         </td><td> 888          </td><td> 754         </td><td> 892          </td><td> 752         </td><td> 890          </td></tr></tbody></table>


<h3>Verification of Group FLOPS_DP with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/FLOPS_DP_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 3704        </td><td> 3743         </td><td> 3740        </td><td> 3783         </td><td> 3732        </td><td> 3779         </td></tr>
<tr><td> 24kB    </td><td> 3759        </td><td> 3780         </td><td> 3781        </td><td> 3801         </td><td> 3777        </td><td> 3797         </td></tr>
<tr><td> 128kB   </td><td> 1956        </td><td> 1973         </td><td> 1979        </td><td> 1986         </td><td> 1973        </td><td> 1979         </td></tr>
<tr><td> 2MB     </td><td> 1471        </td><td> 1470         </td><td> 1472        </td><td> 1471         </td><td> 1471        </td><td> 1471         </td></tr>
<tr><td> 1GB     </td><td> 565         </td><td> 564          </td><td> 572         </td><td> 571          </td><td> 568         </td><td> 567          </td></tr></tbody></table>



<h2>Verification of Group L2</h2>
<h3>Verification of Group L2 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 35908       </td><td> 4            </td><td> 36591       </td><td> 5            </td><td> 36413.00    </td><td> 4.40         </td></tr>
<tr><td> 1MB     </td><td> 21757       </td><td> 21725        </td><td> 21773       </td><td> 21799        </td><td> 21764.80    </td><td> 21770.80     </td></tr>
<tr><td> 4MB     </td><td> 21270       </td><td> 21336        </td><td> 21311       </td><td> 21382        </td><td> 21297.20    </td><td> 21361.80     </td></tr>
<tr><td> 1GB     </td><td> 12612       </td><td> 12638        </td><td> 12615       </td><td> 12644        </td><td> 12613.60    </td><td> 12640.60     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 44983       </td><td> 6            </td><td> 44998       </td><td> 8            </td><td> 44990.60    </td><td> 6.60         </td></tr>
<tr><td> 1MB     </td><td> 17556       </td><td> 35113        </td><td> 17559       </td><td> 35124        </td><td> 17557.60    </td><td> 35118.00     </td></tr>
<tr><td> 4MB     </td><td> 17486       </td><td> 34993        </td><td> 17488       </td><td> 35002        </td><td> 17487.20    </td><td> 34997.00     </td></tr>
<tr><td> 1GB     </td><td> 6732        </td><td> 13219        </td><td> 6737        </td><td> 13233        </td><td> 6734.00     </td><td> 13225.40     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 70591       </td><td> 8            </td><td> 70659       </td><td> 11           </td><td> 70641.20    </td><td> 9.80         </td></tr>
<tr><td> 1MB     </td><td> 22853       </td><td> 34296        </td><td> 22879       </td><td> 34333        </td><td> 22868.20    </td><td> 34314.60     </td></tr>
<tr><td> 4MB     </td><td> 22638       </td><td> 33983        </td><td> 22645       </td><td> 34017        </td><td> 22641.40    </td><td> 34005.60     </td></tr>
<tr><td> 1GB     </td><td> 8403        </td><td> 12485        </td><td> 8426        </td><td> 12514        </td><td> 8416.60     </td><td> 12499.20     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 66965       </td><td> 8            </td><td> 67648       </td><td> 9            </td><td> 67108.60    </td><td> 8.60         </td></tr>
<tr><td> 1MB     </td><td> 22063       </td><td> 29427        </td><td> 22071       </td><td> 29448        </td><td> 22067.40    </td><td> 29438.20     </td></tr>
<tr><td> 4MB     </td><td> 21964       </td><td> 29346        </td><td> 21967       </td><td> 29358        </td><td> 21965.60    </td><td> 29352.40     </td></tr>
<tr><td> 1GB     </td><td> 8991        </td><td> 11951        </td><td> 9083        </td><td> 12016        </td><td> 9041.40     </td><td> 11984.80     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 59804       </td><td> 7            </td><td> 59862       </td><td> 8            </td><td> 59843.00    </td><td> 7.80         </td></tr>
<tr><td> 1MB     </td><td> 23521       </td><td> 29472        </td><td> 23560       </td><td> 29490        </td><td> 23548.00    </td><td> 29480.20     </td></tr>
<tr><td> 4MB     </td><td> 23283       </td><td> 29172        </td><td> 23294       </td><td> 29185        </td><td> 23289.00    </td><td> 29176.60     </td></tr>
<tr><td> 1GB     </td><td> 9146        </td><td> 11423        </td><td> 9244        </td><td> 11506        </td><td> 9175.60     </td><td> 11449.20     </td></tr></tbody></table>


<h3>Verification of Group L2 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L2_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 72768       </td><td> 5            </td><td> 72875       </td><td> 7            </td><td> 72837.40    </td><td> 5.60         </td></tr>
<tr><td> 1MB     </td><td> 29312       </td><td> 29321        </td><td> 29338       </td><td> 29334        </td><td> 29328.80    </td><td> 29329.20     </td></tr>
<tr><td> 4MB     </td><td> 29320       </td><td> 29346        </td><td> 29331       </td><td> 29352        </td><td> 29327.20    </td><td> 29349.20     </td></tr>
<tr><td> 1GB     </td><td> 13241       </td><td> 13032        </td><td> 13269       </td><td> 13072        </td><td> 13254.60    </td><td> 13048.80     </td></tr></tbody></table>


<h2>Verification of Group L3</h2>
<h3>Verification of Group L3 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 36517       </td><td> 4            </td><td> 36552       </td><td> 5            </td><td> 36534.20    </td><td> 4.80         </td></tr>
<tr><td> 1MB     </td><td> 21721       </td><td> 42179        </td><td> 21781       </td><td> 42275        </td><td> 21753.00    </td><td> 42214.20     </td></tr>
<tr><td> 4MB     </td><td> 21287       </td><td> 41457        </td><td> 21321       </td><td> 41573        </td><td> 21307.60    </td><td> 41489.60     </td></tr>
<tr><td> 1GB     </td><td> 12611       </td><td> 23816        </td><td> 12614       </td><td> 23821        </td><td> 12612.80    </td><td> 23818.20     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 44940       </td><td> 6            </td><td> 44993       </td><td> 7            </td><td> 44970.40    </td><td> 6.20         </td></tr>
<tr><td> 1MB     </td><td> 17554       </td><td> 28495        </td><td> 17562       </td><td> 28530        </td><td> 17558.80    </td><td> 28513.00     </td></tr>
<tr><td> 4MB     </td><td> 17481       </td><td> 28383        </td><td> 17488       </td><td> 28394        </td><td> 17485.60    </td><td> 28388.40     </td></tr>
<tr><td> 1GB     </td><td> 6727        </td><td> 12720        </td><td> 6739        </td><td> 12742        </td><td> 6733.20     </td><td> 12727.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 69853       </td><td> 9            </td><td> 70663       </td><td> 11           </td><td> 70497.20    </td><td> 10.00        </td></tr>
<tr><td> 1MB     </td><td> 22864       </td><td> 39650        </td><td> 22881       </td><td> 39690        </td><td> 22873.60    </td><td> 39676.60     </td></tr>
<tr><td> 4MB     </td><td> 22605       </td><td> 39259        </td><td> 22645       </td><td> 39282        </td><td> 22634.80    </td><td> 39271.80     </td></tr>
<tr><td> 1GB     </td><td> 8413        </td><td> 16238        </td><td> 8433        </td><td> 16356        </td><td> 8423.80     </td><td> 16298.40     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 66876       </td><td> 9            </td><td> 67014       </td><td> 10           </td><td> 66966.60    </td><td> 9.20         </td></tr>
<tr><td> 1MB     </td><td> 22053       </td><td> 37417        </td><td> 22068       </td><td> 37538        </td><td> 22062.20    </td><td> 37455.80     </td></tr>
<tr><td> 4MB     </td><td> 21958       </td><td> 37434        </td><td> 21972       </td><td> 37518        </td><td> 21964.80    </td><td> 37480.40     </td></tr>
<tr><td> 1GB     </td><td> 9012        </td><td> 17764        </td><td> 9090        </td><td> 17827        </td><td> 9048.20     </td><td> 17808.20     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 59844       </td><td> 9            </td><td> 59864       </td><td> 9            </td><td> 59854.00    </td><td> 9.00         </td></tr>
<tr><td> 1MB     </td><td> 23548       </td><td> 40753        </td><td> 23556       </td><td> 40802        </td><td> 23551.00    </td><td> 40778.40     </td></tr>
<tr><td> 4MB     </td><td> 23269       </td><td> 40641        </td><td> 23291       </td><td> 40677        </td><td> 23284.80    </td><td> 40666.20     </td></tr>
<tr><td> 1GB     </td><td> 9182        </td><td> 18091        </td><td> 9223        </td><td> 18188        </td><td> 9198.60     </td><td> 18150.80     </td></tr></tbody></table>


<h3>Verification of Group L3 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images//accuracy/westmere1/L3_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 72807       </td><td> 5            </td><td> 72883       </td><td> 5            </td><td> 72842.40    </td><td> 5.00         </td></tr>
<tr><td> 1MB     </td><td> 29318       </td><td> 23368        </td><td> 29333       </td><td> 23383        </td><td> 29326.20    </td><td> 23372.80     </td></tr>
<tr><td> 4MB     </td><td> 29082       </td><td> 23272        </td><td> 29108       </td><td> 23293        </td><td> 29099.20    </td><td> 23281.40     </td></tr>
<tr><td> 1GB     </td><td> 13303       </td><td> 12580        </td><td> 13313       </td><td> 12600        </td><td> 13308.80    </td><td> 12593.00     </td></tr></tbody></table>

