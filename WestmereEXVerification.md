# Hardware description #
Sockets: 4<br>
Cores per socket: 10<br>
Threads per core: 2<br>
Total number of processing units: 80<br>

<h1>Available groups</h1>
Each architecture defines a different set of groups. Here all the groups available for the Intel Westmere EX processor are listed:<br>
FLOPS_X87: X87 MFlops/s<br>
CACHE: Data cache miss rate/ratio<br>
FLOPS_SP: Single Precision MFlops/s<br>
TLB: TLB miss rate/ratio<br>
L2: L2 cache bandwidth in MBytes/s<br>
L3: L3 cache bandwidth in MBytes/s<br>
BRANCH: Branch prediction miss rate/ratio<br>
L2CACHE: L2 cache miss rate/ratio<br>
FLOPS_DP: Double Precision MFlops/s<br>
DATA: Load to store ratio<br>

<h1>Available verification tests</h1>
Not all groups can be tested for accuracy. Here only the groups are listed that can be verified. Each group is followed by the low-level benchmarks that are performed for comparison.<br>
FLOPS_DP: stream, triad<br>
L2: load, store, copy, stream, triad, update<br>
L3: load, store, copy, stream, triad, update<br>

<h1>Accuracy comparison</h1>
For each varification group, the tests are performed twice. Once in a plain manner without measuring but calculating the resulting values and once through an instumented code with LIKWID.<br>
<h2>Verification of Group FLOPS_DP</h2>
<h3>Verification of Group FLOPS_DP with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/FLOPS_DP_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 4532        </td><td> 4515         </td><td> 4543        </td><td> 4604         </td><td> 4538        </td><td> 4592         </td></tr>
<tr><td> 24kB    </td><td> 4498        </td><td> 4549         </td><td> 4557        </td><td> 4596         </td><td> 4532        </td><td> 4578         </td></tr>
<tr><td> 128kB   </td><td> 2082        </td><td> 2257         </td><td> 2149        </td><td> 2341         </td><td> 2128        </td><td> 2321         </td></tr>
<tr><td> 2MB     </td><td> 1426        </td><td> 1625         </td><td> 1434        </td><td> 1632         </td><td> 1430        </td><td> 1629         </td></tr>
<tr><td> 1GB     </td><td> 481         </td><td> 580          </td><td> 482         </td><td> 581          </td><td> 481         </td><td> 580          </td></tr></tbody></table>


<h3>Verification of Group FLOPS_DP with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 24kB               </td><td> 20000             </td></tr>
<tr><td> 128kB              </td><td> 10000             </td></tr>
<tr><td> 2MB                </td><td> 5000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 10 times, hence the first 10 entries on the x-axis correspond to the 10 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/FLOPS_DP_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 2981        </td><td> 3029         </td><td> 3047        </td><td> 3088         </td><td> 3029        </td><td> 3070         </td></tr>
<tr><td> 24kB    </td><td> 3032        </td><td> 3053         </td><td> 3059        </td><td> 3082         </td><td> 3043        </td><td> 3068         </td></tr>
<tr><td> 128kB   </td><td> 1580        </td><td> 1584         </td><td> 1595        </td><td> 1602         </td><td> 1590        </td><td> 1594         </td></tr>
<tr><td> 2MB     </td><td> 1140        </td><td> 1137         </td><td> 1147        </td><td> 1147         </td><td> 1144        </td><td> 1143         </td></tr>
<tr><td> 1GB     </td><td> 348         </td><td> 348          </td><td> 349         </td><td> 351          </td><td> 348         </td><td> 348          </td></tr></tbody></table>


<h2>Verification of Group L2</h2>
<h3>Verification of Group L2 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 29433       </td><td> 4            </td><td> 29458       </td><td> 4            </td><td> 29443       </td><td> 4            </td></tr>
<tr><td> 1MB     </td><td> 16717       </td><td> 16755        </td><td> 16851       </td><td> 16849        </td><td> 16790       </td><td> 16820        </td></tr>
<tr><td> 4MB     </td><td> 16782       </td><td> 16731        </td><td> 16805       </td><td> 16844        </td><td> 16796       </td><td> 16808        </td></tr>
<tr><td> 1GB     </td><td> 5246        </td><td> 5239         </td><td> 5283        </td><td> 5283         </td><td> 5261        </td><td> 5267         </td></tr></tbody></table>


<h3>Verification of Group L2 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 36112       </td><td> 6            </td><td> 36633       </td><td> 7            </td><td> 36319       </td><td> 6            </td></tr>
<tr><td> 1MB     </td><td> 13372       </td><td> 26721        </td><td> 13403       </td><td> 26746        </td><td> 13388       </td><td> 26735        </td></tr>
<tr><td> 4MB     </td><td> 13292       </td><td> 26578        </td><td> 13415       </td><td> 26672        </td><td> 13328       </td><td> 26616        </td></tr>
<tr><td> 1GB     </td><td> 4724        </td><td> 9270         </td><td> 4747        </td><td> 9370         </td><td> 4733        </td><td> 9317         </td></tr></tbody></table>


<h3>Verification of Group L2 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 56511       </td><td> 8            </td><td> 57501       </td><td> 11           </td><td> 57271       </td><td> 9            </td></tr>
<tr><td> 1MB     </td><td> 17747       </td><td> 26632        </td><td> 17852       </td><td> 26717        </td><td> 17782       </td><td> 26666        </td></tr>
<tr><td> 4MB     </td><td> 17578       </td><td> 26377        </td><td> 17695       </td><td> 26493        </td><td> 17624       </td><td> 26431        </td></tr>
<tr><td> 1GB     </td><td> 5956        </td><td> 8830         </td><td> 5965        </td><td> 8872         </td><td> 5961        </td><td> 8851         </td></tr></tbody></table>


<h3>Verification of Group L2 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 53502       </td><td> 8            </td><td> 54379       </td><td> 10           </td><td> 53716       </td><td> 8            </td></tr>
<tr><td> 1MB     </td><td> 17216       </td><td> 22984        </td><td> 17274       </td><td> 23011        </td><td> 17233       </td><td> 23000        </td></tr>
<tr><td> 4MB     </td><td> 17107       </td><td> 22846        </td><td> 17137       </td><td> 22877        </td><td> 17120       </td><td> 22863        </td></tr>
<tr><td> 1GB     </td><td> 5784        </td><td> 7667         </td><td> 5793        </td><td> 7705         </td><td> 5789        </td><td> 7678         </td></tr></tbody></table>


<h3>Verification of Group L2 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 47772       </td><td> 6            </td><td> 48737       </td><td> 8            </td><td> 48330       </td><td> 7            </td></tr>
<tr><td> 1MB     </td><td> 18302       </td><td> 22833        </td><td> 18376       </td><td> 22982        </td><td> 18338       </td><td> 22931        </td></tr>
<tr><td> 4MB     </td><td> 18102       </td><td> 22731        </td><td> 18196       </td><td> 22810        </td><td> 18158       </td><td> 22763        </td></tr>
<tr><td> 1GB     </td><td> 5539        </td><td> 6909         </td><td> 5580        </td><td> 6957         </td><td> 5559        </td><td> 6932         </td></tr></tbody></table>


<h3>Verification of Group L2 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L2_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 58604       </td><td> 4            </td><td> 58759       </td><td> 5            </td><td> 58705       </td><td> 4            </td></tr>
<tr><td> 1MB     </td><td> 23890       </td><td> 24025        </td><td> 24067       </td><td> 24055        </td><td> 24026       </td><td> 24043        </td></tr>
<tr><td> 4MB     </td><td> 23700       </td><td> 23781        </td><td> 23839       </td><td> 23855        </td><td> 23769       </td><td> 23819        </td></tr>
<tr><td> 1GB     </td><td> 8479        </td><td> 8395         </td><td> 8590        </td><td> 8436         </td><td> 8539        </td><td> 8419         </td></tr></tbody></table>


<h2>Verification of Group L3</h2>
<h3>Verification of Group L3 with Test load</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 29365       </td><td> 2            </td><td> 29516       </td><td> 2            </td><td> 29453       </td><td> 2            </td></tr>
<tr><td> 1MB     </td><td> 16683       </td><td> 16607        </td><td> 16862       </td><td> 16838        </td><td> 16765       </td><td> 16705        </td></tr>
<tr><td> 4MB     </td><td> 16668       </td><td> 16813        </td><td> 16738       </td><td> 16859        </td><td> 16699       </td><td> 16835        </td></tr>
<tr><td> 1GB     </td><td> 5259        </td><td> 5268         </td><td> 5284        </td><td> 5292         </td><td> 5271        </td><td> 5280         </td></tr></tbody></table>


<h3>Verification of Group L3 with Test store</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 36188       </td><td> 2            </td><td> 36590       </td><td> 3            </td><td> 36289       </td><td> 2            </td></tr>
<tr><td> 1MB     </td><td> 13422       </td><td> 26525        </td><td> 13464       </td><td> 26582        </td><td> 13435       </td><td> 26560        </td></tr>
<tr><td> 4MB     </td><td> 13308       </td><td> 26375        </td><td> 13367       </td><td> 26434        </td><td> 13344       </td><td> 26414        </td></tr>
<tr><td> 1GB     </td><td> 4755        </td><td> 9109         </td><td> 4770        </td><td> 9127         </td><td> 4762        </td><td> 9117         </td></tr></tbody></table>


<h3>Verification of Group L3 with Test copy</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 57363       </td><td> 4            </td><td> 57538       </td><td> 4            </td><td> 57454       </td><td> 4            </td></tr>
<tr><td> 1MB     </td><td> 17828       </td><td> 26487        </td><td> 17856       </td><td> 26632        </td><td> 17840       </td><td> 26554        </td></tr>
<tr><td> 4MB     </td><td> 17576       </td><td> 26153        </td><td> 17660       </td><td> 26329        </td><td> 17630       </td><td> 26265        </td></tr>
<tr><td> 1GB     </td><td> 5979        </td><td> 8711         </td><td> 6010        </td><td> 8781         </td><td> 5996        </td><td> 8754         </td></tr></tbody></table>


<h3>Verification of Group L3 with Test stream</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 53263       </td><td> 4            </td><td> 54601       </td><td> 4            </td><td> 54239       </td><td> 4            </td></tr>
<tr><td> 1MB     </td><td> 17176       </td><td> 22741        </td><td> 17266       </td><td> 22875        </td><td> 17211       </td><td> 22835        </td></tr>
<tr><td> 4MB     </td><td> 17025       </td><td> 22553        </td><td> 17133       </td><td> 22702        </td><td> 17068       </td><td> 22619        </td></tr>
<tr><td> 1GB     </td><td> 5753        </td><td> 7414         </td><td> 5772        </td><td> 7453         </td><td> 5764        </td><td> 7441         </td></tr></tbody></table>


<h3>Verification of Group L3 with Test triad</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 47107       </td><td> 4            </td><td> 48733       </td><td> 4            </td><td> 48053       </td><td> 4            </td></tr>
<tr><td> 1MB     </td><td> 18340       </td><td> 22706        </td><td> 18370       </td><td> 22751        </td><td> 18356       </td><td> 22730        </td></tr>
<tr><td> 4MB     </td><td> 18091       </td><td> 22367        </td><td> 18128       </td><td> 22399        </td><td> 18107       </td><td> 22376        </td></tr>
<tr><td> 1GB     </td><td> 5570        </td><td> 6730         </td><td> 5580        </td><td> 6736         </td><td> 5576        </td><td> 6733         </td></tr></tbody></table>


<h3>Verification of Group L3 with Test update</h3>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/wesex1/L3_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 57647       </td><td> 2            </td><td> 58929       </td><td> 2            </td><td> 58574       </td><td> 2            </td></tr>
<tr><td> 1MB     </td><td> 23974       </td><td> 23948        </td><td> 24036       </td><td> 24020        </td><td> 24011       </td><td> 23977        </td></tr>
<tr><td> 4MB     </td><td> 23683       </td><td> 23640        </td><td> 23748       </td><td> 23722        </td><td> 23718       </td><td> 23681        </td></tr>
<tr><td> 1GB     </td><td> 8478        </td><td> 8125         </td><td> 8587        </td><td> 8212         </td><td> 8543        </td><td> 8185         </td></tr></tbody></table>
