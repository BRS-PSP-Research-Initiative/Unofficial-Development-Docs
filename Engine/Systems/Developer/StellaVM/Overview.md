# StellaVM Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This is a general overview of what is known about StellaVM.

* Purpose: Virtual Machine to run the full game as separate instance from PSP hardware logic; this aids with porting to other platforms and reusing engine code
* Duties:
    * Replace the standard PSP boot logic with a custom bootstrap
    * Manage all memory allocations beyond what the PSP hardware allows
    * Manage all tasks related to the Event System
* Observations:
    * Most tasks use a 4KB page size (or variation of)
    * Minimum PSP bootloader code is used so that real bootloader and bootstrapping logic gets called to replace it
    * As per decompilation (with some extra checks made due to Ghidra possibly making mistakes): StellaVM allocates 21 MB of memory to house the entire game
    * Part of the Bootloader code stored in the header probably read as the real VM main logic

---
