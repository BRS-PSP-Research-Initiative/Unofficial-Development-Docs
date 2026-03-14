# BXCB Param.bin Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: BRS eXtensive Control Binary
* Type: Management
* Extension: .bin
* Header: BXCB
* Purpose: Battle Module Control Center
* System Equivalent:
    * Field System: SC
* Header Structure
	* 0x04 - 4-byte File Size
	* 0x0c - always 0x20
	* 0x20 - battle model archive id
* Data Structure:
    * Configuration Switchboard (0x10 - 0x64)
    * Debugger (0x200 - 0x231):
        * 0x04 - 1-byte Visual Indicator where the format specification is same as File Size
        * 0x18 - 1-byte Debug Code (uses Sony's Controller codes for displaying status)

---
