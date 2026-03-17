# RTDP Volume Archive Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Real-Time Data Pack
* Type: Data archive
* Extension: .vol
* Header: RTDP
* Purpose: Stores Battle and Engine System Data in a streamable format that allows for rapid Production and loading of contents within
* Notes:
    * Order of File Names related to stage of Production System and which Format does what based on which System VOL archive is used for
* Header Structure:
	* 0x04 - 4-byte Offset to start of Encrypted Data section
	* 0x08 - 4-byte Number of Encrypted Files within Archive
	* 0x0c - 4-byte VOL Archive File Size
	* 0x10 - 1-byte XOR Decryption Key
	* 0x20 - File list starts here; each name takes up 32 bytes
* File List Data Structure:
    * 0x04 - 4-byte Data Offset from start of Address found at 0x04
    * 0x08 - 4-byte Expected Data Size after Decryption

---
