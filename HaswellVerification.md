# Hardware description #
Sockets: 1<br>
Cores per socket: 4<br>
Threads per core: 2<br>
Total number of processing units: 8<br>

<h1>Available groups</h1>
Each architecture defines a different set of groups. Here all the groups available for the Intel Core Haswell processor are listed:<br>
CLOCK: Power and Energy consumption<br>
ENERGY: Power and Energy consumption<br>
TLB: TLB miss rate/ratio<br>
L3: L3 cache bandwidth in MBytes/s<br>
BRANCH: Branch prediction miss rate/ratio<br>
L2CACHE: L2 cache miss rate/ratio<br>
DATA: Load to store ratio<br>

<h1>Available verification tests</h1>
Not all groups can be tested for accuracy. Here only the groups are listed that can be verified. Each group is followed by the low-level benchmarks that are performed for comparison.<br>
L3: load, store, copy, stream, triad, update<br>

<h1>Accuracy comparison</h1>
For each varification group, the tests are performed twice. Once in a plain manner without measuring but calculating the resulting values and once through an instumented code with LIKWID.<br>
<h2>Verification of Group L3 with Test load</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 7500              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_load.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 81670       </td><td> 4            </td><td> 81956       </td><td> 10           </td><td> 81812.40    </td><td> 7.00         </td></tr>
<tr><td> 1MB     </td><td> 40509       </td><td> 39289        </td><td> 41198       </td><td> 41414        </td><td> 40981.00    </td><td> 40908.20     </td></tr>
<tr><td> 4MB     </td><td> 40048       </td><td> 39932        </td><td> 41326       </td><td> 41319        </td><td> 40687.40    </td><td> 40810.80     </td></tr>
<tr><td> 1GB     </td><td> 16888       </td><td> 16731        </td><td> 17409       </td><td> 17378        </td><td> 17203.20    </td><td> 17041.80     </td></tr></tbody></table>


<h2>Verification of Group L3 with Test store</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_store.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 52975       </td><td> 3            </td><td> 53150       </td><td> 5            </td><td> 53092.40    </td><td> 3.60         </td></tr>
<tr><td> 1MB     </td><td> 25168       </td><td> 45822        </td><td> 25195       </td><td> 47077        </td><td> 25181.20    </td><td> 46185.20     </td></tr>
<tr><td> 4MB     </td><td> 25019       </td><td> 44509        </td><td> 25139       </td><td> 45700        </td><td> 25088.20    </td><td> 45422.60     </td></tr>
<tr><td> 1GB     </td><td> 9639        </td><td> 15810        </td><td> 9877        </td><td> 16500        </td><td> 9747.60     </td><td> 16009.40     </td></tr></tbody></table>


<h2>Verification of Group L3 with Test copy</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_copy.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 101938      </td><td> 6            </td><td> 102747      </td><td> 14           </td><td> 102313.40   </td><td> 9.80         </td></tr>
<tr><td> 1MB     </td><td> 32508       </td><td> 44498        </td><td> 32655       </td><td> 45102        </td><td> 32585.40    </td><td> 44795.20     </td></tr>
<tr><td> 4MB     </td><td> 31983       </td><td> 43379        </td><td> 32570       </td><td> 44818        </td><td> 32317.40    </td><td> 44334.20     </td></tr>
<tr><td> 1GB     </td><td> 12743       </td><td> 17080        </td><td> 13051       </td><td> 17347        </td><td> 12949.60    </td><td> 17264.00     </td></tr></tbody></table>


<h2>Verification of Group L3 with Test stream</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_stream.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 87434       </td><td> 6            </td><td> 101118      </td><td> 7            </td><td> 98085.60    </td><td> 6.60         </td></tr>
<tr><td> 1MB     </td><td> 36474       </td><td> 44212        </td><td> 36552       </td><td> 44664        </td><td> 36519.40    </td><td> 44497.00     </td></tr>
<tr><td> 4MB     </td><td> 35986       </td><td> 44071        </td><td> 36546       </td><td> 44426        </td><td> 36230.40    </td><td> 44273.80     </td></tr>
<tr><td> 1GB     </td><td> 14216       </td><td> 17095        </td><td> 14441       </td><td> 17247        </td><td> 14350.20    </td><td> 17176.80     </td></tr></tbody></table>


<h2>Verification of Group L3 with Test triad</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_triad.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 101321      </td><td> 7            </td><td> 101819      </td><td> 8            </td><td> 101545.80   </td><td> 7.20         </td></tr>
<tr><td> 1MB     </td><td> 38859       </td><td> 44344        </td><td> 38977       </td><td> 44484        </td><td> 38914.40    </td><td> 44431.20     </td></tr>
<tr><td> 4MB     </td><td> 37835       </td><td> 43019        </td><td> 39003       </td><td> 44285        </td><td> 38550.00    </td><td> 43810.60     </td></tr>
<tr><td> 1GB     </td><td> 14557       </td><td> 17227        </td><td> 15179       </td><td> 17412        </td><td> 15025.20    </td><td> 17327.00     </td></tr></tbody></table>


<h2>Verification of Group L3 with Test update</h2>
<table><thead><th> <b>Stream size</b> </th><th> <b>Iterations</b> </th></thead><tbody>
<tr><td> 12kB               </td><td> 20000             </td></tr>
<tr><td> 1MB                </td><td> 10000             </td></tr>
<tr><td> 4MB                </td><td> 2000              </td></tr>
<tr><td> 1GB                </td><td> 50                </td></tr></tbody></table>

Each data size is tested 5 times, hence the first 5 entries on the x-axis correspond to the 5 runs for the first data size of 12kB and so on.<br>
<img src='http://likwid.googlecode.com/svn/wiki/images/accuracy/heidi/L3_update.png' />

<table><thead><th> Variant </th><th> Plain (Min) </th><th> LIKWID (Min) </th><th> Plain (Max) </th><th> LIKWID (Max) </th><th> Plain (Avg) </th><th> LIKWID (Avg) </th></thead><tbody>
<tr><td> 12kB    </td><td> 104674      </td><td> 3            </td><td> 104925      </td><td> 5            </td><td> 104779.00   </td><td> 3.40         </td></tr>
<tr><td> 1MB     </td><td> 45309       </td><td> 30634        </td><td> 47856       </td><td> 31064        </td><td> 47010.60    </td><td> 30843.20     </td></tr>
<tr><td> 4MB     </td><td> 46965       </td><td> 30556        </td><td> 47646       </td><td> 30973        </td><td> 47347.80    </td><td> 30748.60     </td></tr>
<tr><td> 1GB     </td><td> 19537       </td><td> 15512        </td><td> 19731       </td><td> 15594        </td><td> 19663.40    </td><td> 15569.00     </td></tr>