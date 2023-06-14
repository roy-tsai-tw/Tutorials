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

## Problem 2. Some Findings about LiteX
* The file "generate_renode_scripts.py" in the path " /home/usr_name/CFU-Playground/scripts/ " is the script to generate the file "digilent_arty.resc" in the folder "/home/usr_name/CFU-Playground/proj/my_first_cfu/build/renode/".
* The file "core.py" in "/home/usr_name/CFU-Playground/third_party/python/litex/litex/soc/cores/cpu/vexriscv/" is the VexRiscV CPU python model in LiteX.
* The file "./soc/build/digilent_arty.my_first_cfu/gateware/digilent_arty.v" is the top soc module before synthesis.
* The file "./soc/build/digilent_arty.my_first_cfu/csr.json" records the memory mapping of all components on liteX SoC.

## Problem 3. Some errors I've encountered during make renode/make load phase after changing a big model for profiling on VexRiscv. 
* The following are some errors you may see from the terminal:
```
TfLiteStatus invoke_status = interpreter.Invoke(); Failed
Model allocation started before finishing previously allocated model.
```
* Solution: Change the size of kTensorArenaSize in "/home/user_name/CFU-Playground/common/src/tflite.cc" to make it bigger, i.e. from 15 * 1024 to 60 * 1024.

## Problem 4. Make renode failed with the message "c++: fatal error: Killed signal terminated program cc1plus."
* The reason is that your modle is too big such that your RAM is not enough for compiling.
* Solution: Wait it until it stop and make renode again, then it will continue to compile other C files.

