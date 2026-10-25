# RVLS Format Docs

---

*Copyright 2026 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Recursive Volume Listed Storage
* Type: Installation
* Extension: .vls
* Header: RVLS
* Purpose: Contains a list of all Archives on Disc that must be stored on a Memory Card for faster loading
* System Equivalent:
  * Debug System: RVLX (not found in retail release)
* Header Structure:
  * 0x08 - 4-byte List Length
  * 0x0c - 4-byte GUID (?)
  * 0x10 - 4-byte Buffer Size (in KB)
  * 0x20 - 32-byte DATA_START.BIN string
---
