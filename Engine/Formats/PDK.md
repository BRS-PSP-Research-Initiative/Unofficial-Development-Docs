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
  * 0x04 - 2-Byte Table Size
	* 0x06 - 2-Byte Offset to first SSCR section
  * 0x08 4-byte Index * Offset + <0x06> - Address where PDK section ends with each Index being tied to a 8-byte entry in table
  * 0x0c 4-byte Index * Offset - Size of section
---
