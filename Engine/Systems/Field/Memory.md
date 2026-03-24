# Field Memory Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is for aiding in the understanding of how the Field System handles its top-level Memory allocation.

* General Allocation Regions:
    * Data Buffer:
        * Shared with Battle System when switching from Field to Battle
        * Holds all Data that will be passed to other Systems, most often products of Assembly step
    * Assets Buffer:
        * Shared with Battle and other Systems related to current Stage
        * Region where relevant Game Assets from disc are loaded in and stored
        * Stores full SC container data after extracting from GZip Compressed archive on Disc
    * Pointer Buffer:
        * Special region at offset 0x20000 for storing Pointers related to both Buffers
* Notable Regions:
    * Data Buffer:
        * Top Level SC blob and SSCR scripting region make up the front of this region
        * Pointer 0x20028 - Atrac3 Audio Data
        * Pointer 0x20014 - List Data
        * Pointer 0x232e0 - Field Event sub-System
    * Assets Buffer:
        * 0x1d00-0x2000 - Good indication of working with SC data; varies depending on purpose and structure
        * 0x5000+:
            * Special region shared with Battle System
            * Can also be used as an overflow if SC data is too large (frequently happens due to most being substantially larger)

---
