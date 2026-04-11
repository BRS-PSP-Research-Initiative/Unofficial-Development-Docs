# Heap Allocation Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Purpose: Provide a reference to how Game Heap Memory is Allocated
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
            * 0x20014 - Save File on Memory Card Table
            * 0x20018 - At3 Data
            * 0x20030 - 4-byte Glare Effect Callback
            * 0x20034 - 4-byte Blur Effect Callback
            * 0x20050 - 4-byte RecMsgTask Callback
            * 0x20054 - 4-byte GloDatTask Callback
            * 0x206bc - Assets Data
            * 0x209dc - Unknown
            * 0x209e0 - 4-byte sceKernelSubIntr_handler_count
            * 0x209e4 - 4-byte Continue Game Flag
            * 0x209e8 - 8-byte Input Stream Delimiter
            * 0x21528 - Copy of 0x21a10
            * 0x21a10 - 0x100-byte Projection Matrix Data
            * 0x21a74 - 0x400-byte Player Character Data

---

