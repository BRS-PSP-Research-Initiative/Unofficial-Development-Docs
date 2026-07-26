# Heap Allocation Doc

---

*Copyright 2026 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Purpose: Provide a reference to how Game Heap Memory is Allocated in the binary
* Definitions (can be used to determine what type of data is being worked with when only offsets and base pointer are known in decompilation):
  * Unnamed Section - System specific heap data
  * Production Heap - Section of data that goes directly into the gameplay experiences
  * Assets Heap - Currently loaded Assets from disc based on context (often the System being called upon is enough)
* Allocation:
    * Pointer Table:
        * Offset from 0 address on Heap:
            * 0x00008 - Unknown
            * 0x0000c - 1-byte Possible Debug Mode Switch
            * 0x00018 - MS_DataSave data (if `page size` is 0)
            * 0x0001c - MS_DataSave data (if `page size` is 2)
            * 0x00020 - StellaVM Event Task callback function
            * 0x00030 - Memory Card data
            * 0x00040 - StellaVM Heap Allocation Stage1 Callback function
            * 0x00054 - Unknown
            * 0x0005c - Unknown
            * 0x000d8 - Unknown
            * 0x00144 - Unknown flag
            * 0x00318 - Flag of some type related to 0x8
            * 0x00598 - INSTDAT.VLD data
            * 0x01000 - TransData data
        * Offset from Production Heap:
            * 0x00004 - 4-byte sceDisplayWaitVblank Mode
            * 0x20014 - 4-byte Save File on Memory Card Table
            * 0x20018 - 4-byte At3 Data
            * 0x2001c - 4-byte Unknown Data
            * 0x20024 - Unknown
            * 0x20028 - Unknown
            * 0x2002c - 4-byte MS Callback Pointer (can change based on context)
            * 0x20030 - 4-byte Glare Effect Callback
            * 0x20034 - 4-byte Blur Effect Callback
            * 0x20038 - 4-byte Stencil Buffer Table Entry (spec)
            * 0x20044 - 4-byte 0x2002c Sanity Check Callback
            * 0x20048 - 4-byte ResultBtlTask Callback
            * 0x20050 - 4-byte RecMsgTask Callback
            * 0x20054 - 4-byte GloDatTask Callback
            * 0x20058 - 4-byte bscr Script Start (Battle)
            * 0x20370 - 4-byte Stencil Buffer Heap (spec)
            * 0x206bc - 4-byte Assets Data
            * 0x20740 - 4-byte Combat Actor ID Table Start
            * 0x20764 - 2-byte Combat Actor HP Table Start
            * 0x2076c - Unknown Pointer used to jump to an Index-based entry in table
            * 0x2077c - Unknown
            * 0x209dc - Unknown
            * 0x209e0 - 4-byte sceKernelSubIntr Handler Count
            * 0x209e4 - 4-byte Continue Game Flag
            * 0x209e8 - 4-byte PC ID
            * 0x21538 - 0x64-byte Projection Matrix Data
            * 0x2159c - 0x400-byte Player Character Data
            * 0x21a10 - Copy of 0x21538
            * 0x21a74 - Copy of 0x2159c
            * 0x21e74 - 4-byte FCHR Data
            * 0x21e76 - 1-byte Hierachy Flag
            * 0x21e77 - Unused Flag
            * 0x21e78 - 1-byte PC Alive Flag
        * Offset from Assets Heap:
            * 0x00044 - Unknown
            * 0x00080 - Unknown
            * 0x00114 - Unknown
            * 0x00180 - Unknown Flag
            * 0x00920 - 4-byte Start to Camera Table (spec)
            * 0x00924 - Unknown
            * 0x00928 - Unknown
            * 0x00bd4 - Unknown
            * 0x00bd8 - Unknown
            * 0x00bdc - Unknown
            * 0x00c34 - Unknown Flag
            * 0x00c4c - 4-byte Copy of 0x00c34
            * 0x00d4c - Unknown
            * 0x00d50 - Unknown
            * 0x00d54 - Unknown
            * 0x00d58 - Unknown
            * 0x00d5c - Unknown
            * 0x00d60 - Unknown
            * 0x00d64 - Unknown
            * 0x00d68 - Unknown
            * 0x00d6c - Unknown
            * 0x00d70 - Unknown
            * 0x00d80 - Unknown
            * 0x00d84 - Unknown
            * 0x00e18 - Unknown
            * 0x00e24 - Unknown
            * 0x00e28 - Unknown
            * 0x00e6c - Unknown
            * 0x00e90 - Unknown
            * 0x00e9c - Unknown
            * 0x01d28 - Unknown
            * 0x01d4c - Enemy Script pointer (spec)
            * 0x01dd8 - 4-byte Unknown
            * 0x021a4 - Unknown
            * 0x04c54 - Transformation / Rotation / Coordinates Float data pointer (not sure which one yet); possibly stores other types of data
            * 0x04ca8 - Unknown
            * 0x05374 - Unknown
            * 0x05378 - Unknown
            * 0x05384 - Unknown
            * 0x05388 - Unknown
            * 0x12074 - With other Offsets = Mask Flag
            * 0x12110 - 4-byte Debug Memory Usage (by Divisor)

---

