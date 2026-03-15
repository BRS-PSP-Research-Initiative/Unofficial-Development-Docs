# PPHD Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Production Header Data
* Type: Production
* Extension: .phd
* Header: PPHD, PPTN, PPPG, PPVA
* Purpose: Provides Asset Production Assembly instructions
* Notes:
    * Probably parsed as a detached Header section of same basename PBD Format file
* Sections:
	* PPHD (Packed Production Header Data)
    * Purpose: Starting point for parsing data
    * Data Structure:
		* 0x04 - Unknown 4-byte value consistent with all PHD files, so it may be a version tag
		* 0x10 - Jump table for the rest of the data with 4-byte entries
	* PPPG (Packed Production Pixel Graph)
    * Purpose: Most likely related to Assembling Pixel Data
    * Data Structure:
		* 0x20 - 4-byte Address offset from PPHD section to an Unknown 4-byte value
	* PPTN (Packed Production Texture Node)
    * Purpose: Most likely related to Assembling Texture Data
    * Data Structure:
		* 0x04 - 4-byte unknown value
		* 0x08 - 4-byte unknown value
		* 0x34 - 4-byte unknown value
		* Rest of data looks like it may be pointers
	* PPVA (Packed Production Vector Assembly)
        * Purpose: Most likely related to Assembling Vector Data (rotation, size, scale, etc)
        * Data Structure:
            * Almost identical layout to PPTN

---
