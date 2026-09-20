# EGXD Format Docs

---

*Copyright 2026 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Enemy Group eXternal Debug
* Type: Debug Data
* Extension: .dat
* Header: EGXD
* System Equivalent:
    * Battle: EGTB
* Purpose: Functions just like EGTB but with extra debug flags and data
* Notes:
  * Stripped from retail release but Game Binary still has enough functionality for reading and parsing them that one could theoretically rebuild part of the format
* Header Structure:
  * 0x40 - 2-byte Debug Entry Count; Stop - 0x0 or 0x7f or line count > 8
---
