# PBD Data Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Packed Bitmap Data
* Type: Asset Data
* Extension: .pbd
* Magic Header: 
		* Packed: Variable 4-byte with at least one single Ascii Character
		* Unpacked: SBS - Sprite Bitmap Stream
* Purpose: Coordinate the reconstruction of Bitmap data that has been packed into a PTMD packed texture file
* Header Structure:
	* 0x04 (2 bytes) - U ID
	* 0x08 - X ID + 0x01

* Notes on IDs
	* X ID correlates to an associate XTC that contains text data will be rendered to the screen
	* U ID is shared with an associated SDOa at 0x04
---
