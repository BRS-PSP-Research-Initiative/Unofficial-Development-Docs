# EGTB Format Docs

---

*Copyright 2026 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Enemy Group Table Binary
* Type: Data
* Extension: .dat
* Header: EGTB
* System Equivalent:
    * Debug: EGXD (not found in retail release)
* Purpose: Stores data related to Enemy Spawn rates, Amounts per Battle, etc
* Notes:
* Header Structure:
  * 0x08: 4-Byte File Size (with byte alignment added; may not be the file size in RTDP Vol)
	* 0x0c - 2-byte Table Range
  * 0x10 - 4-byte Offset to Table Start
---
