# EDXD Data Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Event Driven eXterior Data
* Type: Event
* Extension: .edx
* Header: EDXD
* Purpose: Be the driver for the BATTLE TASK Event System
* Notes:
    * File Size: 1.5kb (hardcoded for of its Type)
    * Always found with an associated same Basename (part before extension) .bms file
* Header Structure:
	* (spec) - Following [PMF format docs](https://hitmen.c02.at/files/yapspd/psp_doc/chap26.html#sec26.8), if you bitwise shift left by 1 byte, the following addresses become possible resolution values:
		* 0x10 - always 0x3c = 60; as 0x3c0 = 960
		* 0x12 - always 0xb4 = 180; as 0xb40 = 2880
		* 0x14 - always 0x1e = 30; as 0x1e0 = 480
		* 0x18 - always 0x14 = 20; as 0x140 = 320
	* 0x5c - Shared value among most if not all edx files - 8FED8D55

---
