# Battle Memory Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is for aiding in the understanding of how the Battle System handles its Memory allocation.

* General Allocation Regions:
    * Data Buffer:
        * Shared with Field Memory when switching out of Battle back to the Field
        * Holds all Data that will be passed to other Systems, most often products of Assembly step
    * Assets Buffer:
        * Shared with Field and other Systems related to current Stage
        * Region where relevant Game Assets from disc are loaded in and stored
        * Currently unknown how much is preloaded and when
* Notable Regions:
    * Data Buffer:
        * BXCB Data and Scripting Blob appear at the very beginning
    * Assets Buffer:
        * 0x0 - Starts at Data Buffer offset 0x206bc
        * 0x21a4 - Currently loaded mdl Asset
        * 0x5000+:
            * Special region shared with Field System
            * Frequently used for large Asset decompression
            * Can also act as temporary storage for parts of Assembly and Production


---
