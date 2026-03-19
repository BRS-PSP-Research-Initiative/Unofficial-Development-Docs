# PDK Mini-Game Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Playable Data Kit
* Type: Data archive
* Extension: .pdk
* Header: PDK
* Purpose: Minigames Module Micro and Macro Control Center
* Notes:
    * Modified version of Field Event sub-System flavor of SC Format
* Header Structure:
	* 0x06 - 4-byte Address to SSCR section
    * 0x0C:
        * 4-byte Offset + 0x06 - Address where PDK section ends
        * Start of 0x4 separated Offset Table for each Section

---
