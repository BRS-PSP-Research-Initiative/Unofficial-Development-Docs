# BXCB Format Docs

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
* Purpose: Configures and drives Systems that rely on a central configuration; Acts as a Control Center in a Production System Architecture
* System Equivalent:
    * Field System: SC (Top Level Only)
    * Engine System: EGXD / EGTB
* Notes:
    * Binary doesn't just check Magic Header by characters like most formats; the Generic File Loader has a check for `0x42435842`, the binary representation
    * Utilizes the PSP's builtin caching system for flushing data
* Header Structure
	* 0x04 - 4-byte File Size
  * 0x08 - 4-byte Debug Flag (?); can be 0 or 0x10
  * 0x0c - 4-byte Table Start
  * 0x10 - 4-byte Table Offset Size
  * 0x14 - 4-byte Table Size (for parsing data)
  * 0x18 - 4-byte Offset to Implementation Section (similar to StellaScript's)
  * 0x1c - 4-byte Unknown Flag
  * 0x20 - 4-byte Unknown Flag
  * When only the Third Entry In Table (used for heap):
    * 0x24 - 4-byte First Table Jump
    * 0x28 - 4-byte Second Table Jump
    * 0x2c - 4-byte Third Table Jump
    * 0x30 - 4-byte Fourth Table Jump
* Data Structure:
    * Configuration Switchboard (0x10 - 0x68)
    * Debugger (0x200 - 0x231):
        * 0x04 - 1-byte Visual Indicator where the format specification is same as File Size
        * 0x18 - 1-byte Debug Code (uses Sony's Controller codes for displaying status)

---
