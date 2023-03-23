# CFU-Playground
## Problem 1. Perf counters not enabled. 
* The guidance showed that after typing "make renode" or "make load", there should be somethin like:
```
Counter |  Total | Starts | Average |     Raw
---------+--------+--------+---------+--------------
    0    |   113M | 124418  |   908   |    113064622
    1    |     0  |     0  |   n/a   |            0
    2    |     0  |     0  |   n/a   |            0
    3    |     0  |     0  |   n/a   |            0
    4    |     0  |     0  |   n/a   |            0
    5    |     0  |     0  |   n/a   |            0
    6    |     0  |     0  |   n/a   |            0
    7    |     0  |     0  |   n/a   |            0
```
  If the table is not shown, the solution is to change "perf.h" in "~/CFU-Playground/common/src/" folder:
```
#define CONFIG_CPU_PERF_CSRS
```
  Add the above line before the following sections:
```
#ifdef CONFIG_CPU_PERF_CSRS
#define NUM_PERF_COUNTERS 8
#else
#define NUM_PERF_COUNTERS 0
#endif
```
  then the table will show up automatically. 

## Problem 2.  
