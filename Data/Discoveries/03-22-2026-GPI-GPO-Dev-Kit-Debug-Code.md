# Theoretical GPO/GPI Debug Exploit Documentation

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Date Found: 03/22/2026
* Time: 11:20 PM CST
* Regions Affected: jpn, usa, eur
* Description: In the Main Thread Callback, the Flushing Mechanism, and an unknown UMD focused function, an extremely rare Sony Devkit Debug implementation was found in the code.
* Source: [PPSSPP Wiki](https://www.ppsspp.org/docs/psp-hardware/other/gpi-gpo/)
* Switches Used:
    * 0: When Main Thread Callback and Flushing both are called
    * 5: During the Dead Master Tutorial and when the main Game is loaded
* Findings:
    * PPSSPP can turn on GPI Switches
    * When using the LED overlay, these things occur:
        * Index 5 flashes during the Dead Master Tutorial and during early loading screens; may apply to all Loading screens since unknown code only runs while the UMD is being read
        * Midway through the first In-Engine Cutscene where Stella awakens in San Francisco (happens between the Soldier walking through smoke and first character with speaking role starts shooting truck), Index 5 switches off completely while main game loop is running
    * Main Thread Callback saves a modified copy of sceKernelGetGPI() to the Production Data stack
* Exploit Vectors:
    * Both Main Thread Callback and the Flushing Mechanism have large surface areas for performing ACE or Pointer Manipulation
    * Flushing Mechanism specifically handles at least the initial Field Data pointer construction; it's suspected the Interface Data Pointer is in the same block
    * Dead Master Tutorial doesn't perform the GPI/GPO checks the Main Gameplay Loop does
    * Save Game Memory Card Data Manipulation
    * Anything else outside of the main Gameplay Loop
* Theoretical Exploit Steps:
    * Force sceKernetGetGPI() to return 1 instead of 0
    * Flag gets passed to Production Data offset 0xc
    * Implementations that call Production Data offset 0xc will activate Debug stuff on Index 5 Switch while Gameplay Loop is active
* Current Limitations:
    * Implementations using exploitable flag have not been found yet
    * Unknown if Debug implementation tied to it was removed by developers before release
    * If source can be believed, cannot be exploited on Consumer Grade Hardware without modifications
    * External tools that can interact with PPSSPP's GPI/GPO Debug Implementation may not be available or functional on platforms other than Windows

---

## Exploit code Snippets:
### Main Thread Callback Exploit Function
```
int sceKernelGPI_exploit_vector(uint range)

{
  int GPI;
  
  if ((-1 < (int)range) && ((int)range < 8)) {
    GPI = sceKernelGetGPI();
    return GPI >> (range & 0x1f);
  }
  return 0;
}
```

### Main Thread Callback (code in between removed for simplicity and relevance)
```
flush_system_memory();
data = get_production_data_blob();
temp = sceKernelGPI_exploit_vector(0);
*(uint *)(data + 0xc) = *(uint *)(data + 0xc) & 0xffffffef | (temp & 1) << 4;
```

### Unknown Code Internal Function
```
void DevKit_GPI_GPO_debug_hardware_switches(int range)

{
  if ((-1 < range) && (range < 8)) {
    sceKernelGetGPI();
    sceKernelSetGPO();
  }
  return;
}
```

### Unknown Code (while UMD is being read)
```
DevKit_GPI_GPO_debug_hardware_switches(5);
sceKernelSignalSema();
if (state_int == 1) {
    state = is_Umd_currently_in_use();
    state_int = CONCAT31(extraout_var_01,state);
}
```
