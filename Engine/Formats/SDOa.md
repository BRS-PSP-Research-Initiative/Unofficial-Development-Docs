# SDOa Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: System Data Object array
* Type: Command Center
* Extension: None known
* Header: SDOa
* System Equivalent:
  * Battle: BXCB
* Purpose: Configures and drives different parts of the LPK
* Notes:
  * Mostly found in System Interface implementations
* Header Structure:
	* 0x04 - 2-byte U ID
  * 0x06 - 2-byte Embedded PTMDs Count
  * `if_btlsys.lpk` (Top Level only)
    * 0x5a0 - 4-byte Configuration Switchboard
  * `if_rsdsys.lpk` (LPK offset <0x54> from Top Level)
    * 0x1438 - 4-byte Configuration Switchboard

* Notes on IDs
    * U ID is shared with an associated DAT object at 0x04
---
