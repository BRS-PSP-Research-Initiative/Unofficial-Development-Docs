# StellaVM Exploit Documentation

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Date Found: 03/24/2026
* Time: 07:15 AM CST
* Regions Affected: jpn, usa, eur
* Description: Within the Save System stack, some Tasks for handling Save File transactions and Game Installation are handled with StellaVM byte-compiled Data found in Data on Disc.
* Current Limitations:
    * Implementations using exploitable flag have not been found yet
    * Unknown if Debug implementation tied to it was removed by developers before release
    * If source can be believed, cannot be exploited on Consumer Grade Hardware without modifications
    * External tools that can interact with PPSSPP's GPI/GPO Debug Implementation may not be available or functional on platforms other than Windows

---

## Exploit code Snippets:
### Initial Functionality
```
void run_StellaVM_byte_compiled_task_callback
            (int heap,undefined4 size,undefined4 subcontext1,undefined4 subcontext2)
{
 undefined4 task;
 
 task = task_callback_heap;
 task_callback_heap = heap;
 set_tbl_data(heap);
 (**(code **)(heap + 0x18))(heap,size,subcontext1,subcontext2);
 task_callback_heap = task;
 return;
}

```

### Heap Allocation Usage (1-byte Heap Allocation to Check Sanity; 4096-byte (4KB) Heap Allocation for full Function)
```
undefined4 run_MS_DataTask_StellaVM_byte_compiled_task_callback(int heap)
{
 int temp;
 
 temp = run_StellaVM_byte_compiled_task_callback(heap,4096,0,0);
 if (temp != 0) {
   MS_DataTask_heap = run_StellaVM_byte_compiled_task_callback(heap,4097,0,0);
   return 1;
 }
 return 0;
}
```

