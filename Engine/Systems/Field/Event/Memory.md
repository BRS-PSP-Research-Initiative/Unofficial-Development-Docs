# Field Event Memory Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is for aiding in the understanding of how the Field System Event implementation handles its Memory allocation.

* Data Region:
    * 0x00 - Shares the same Data Start point as the Minigame System
* Notable Offsets / Regions:
    * 0x73e18 - Audio Data End Flag (can be either 0xffffffff or another value)

---
