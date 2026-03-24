# Player Character Memory Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is for aiding in the understanding of how the Battle System handles its Memory allocation.

* General Allocation Regions:
    * Production:
    * Assets:
* Notable Regions:
    * Production:
        * Pointer 0x2159c - 0x400-byte Player Character Data
    * Assets:
        * 0x403 - Menu Data (might be global or shared with other systems)
        * 0x544 - EDXD Asset
        * 0xe24 - Start of what is most likely the AI Scripting Table
        * 0x1d4c - Copy of 0xe24
        * 0x21a4 - Currently loaded MDL Asset
        * 0x5000+:
            * Special region shared with Field System
            * Frequently used for large Asset decompression
            * Can also act as temporary storage for parts of Assembly and Production

---
