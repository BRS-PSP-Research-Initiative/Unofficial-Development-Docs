# XTC Interface Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Tentative Name: Extensible Text Container
* Type: Container
* Extension: .xtc
* Header: XTC
* Purpose: Render text on screen
* Notes:
  * (July 2026 Notes):
    * Possibly an undocumented variant of the XTC comic book format used and created for some obscure web mangas from the time period of release; [source](https://github.com/CrazyCoder/crengine-ng/blob/main/crengine/docs/XtcFormat.md) *NOTE: spec sheet AI generated and most tools following suit; possibly incorrect but also outside scope to fully dissect the format*
    * ImageEpoch was originally a digital art and 3D asset production studio before independent game development started, further making this a likely scenario
	* Primarily related to user interface elements
	* Files can vary in size on disc depending on region and language
	* Text is allocated to the end of the data structure
* Data Typings:
	* \b(#) - Button text with event tied to it (such as changing a setting or zooming the camera in or out in the Gallery)
	* \z(#) - Zone text; zones include time of day variants of game stages
	* Untyped - Readable but not interactive
* Header Structure:
    * 0x04 - 4-byte File Size
	* 0x08 - 4-byte X ID
    * 0x10:
        * if not 0xFF / 0x00 - 4-byte Address of main Data Blob

---
