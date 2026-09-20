# SCMP Container Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Stage Container MultiPlayer
* Type: Container
* Header: SCMP
* Purpose: Designates Map and Field Character as part of scrapped Multiplayer mode
* Notes:
	* Found in multiple `MAP_D_STG_02` (New York) maps, suggesting that those were mostly designed with this mode in mind
	* ZIG Multiplayer Character:
		* Seems to be the only SC container that doesn't have an SSCR section but instead contains an extra SCMP section in its place
		* Contains 3 SCMP headers total
		* Shares the same Namespace as the BRS model (`_P_`)
		* Has almost as many bones as most of the BRS models and contains some Animation data (but not the same way to access it as most other models minus some equipment, gadgets and skills)
		* The 0x20 math calculations (see my INSA notes on that part) for the second bone are bugged; their final result seems to be one of the few inconsistencies among the models
* Header Structure (mostly follows SC Format structure):
  * 0x02 - (spec) Hierarchy flag not set in Data; gets set in Game Binary when parsing an SCMP within one of the New York (Stage 2) Maps
---
