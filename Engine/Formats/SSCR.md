# SSCR Scripting Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Self-contained SCRipting module
* Type: Field Scripting
* Extension: .ss
* Header: SSCR
* Purpose: Contains Scripting System names but not Instructions or Implementation data
* System Equivalent:
    Battle System: bscr
* Notes:
	* This was first discovered on a random hunch while out for food. A quick script to check for vertex values found BRS's model pretty quickly under the `BTL\FLD\FCHR` directory
	* Often found inside of SC containers
* Structure:
	* 0x0c - Scripted Data Section Start
	* 0x10 - Scripted Data String End Address
	* 0x14 - Scripted Data Section End Address
	* 0x18 - Relative Offset to End of Data Chunk
    * 0x20-0x50 - Possible Padding before Script Names Table
---
