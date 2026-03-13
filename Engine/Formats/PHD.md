# PPHD Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Packed Header Data
* Type: Data
* Extension: .phd
* Header: PPHD, PPTN, PPPG, PPVA
* Purpose: Currently Unknown
* Notes:
	* These all seem to be linked together in multiple VOL archives in a set structure
* Header Structure:
	* PPHD (Packed Pixel Header Data)
		* 0x04 - Unknown 4-byte value consistent with all PHD files, so it may be a version tag
		* 0x10 - Jump table for the rest of the data with 4-byte entries
	* PPPG (Packed Pixel Pixel Graph)
		* 0x20 - 4-byte jump from PPHD to a 4-byte value
	* PPTN (Packed Pixel Texture Node)
		* 0x04 - 4-byte unknown value
		* 0x08 - 4-byte unknown value
		* 0x34 - 4-byte unknown value
		* Rest of data looks like it may be pointers
	* PPVA (Packed Pixel Vector Animation)
		* Almost identical layout to PPTN
---
