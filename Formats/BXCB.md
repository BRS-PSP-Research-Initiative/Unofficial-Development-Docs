# BXCB Param.bin Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: BRS eXtensive Control Binary
* Type: Data
* Extension: .bin
* Header: BXCB
* Purpose:
    * Param1.bin - Unknown
    * Param2.bin - Data driven orchestration in a State Machine
* Header Structure (shared):
	* 0x04 - data file size
	* 0x0c - always 0x20
* Header Structure (param1.bin):
	* 0x20 - battle model archive id
* Header Structure (param2.bin):
    * 0x10 - 0xB0 - State alteration switchboard; each 4-byte chunk can cause different processes to occur based on which system is driving the data when and why
---
