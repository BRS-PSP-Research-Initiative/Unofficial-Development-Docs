# Audio Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a general overview of the entire Audio System.

* Purpose: Handle the audio of everything in the game.
* Real-Life Counterpart: Sound studio
* Notes:
    * The audio format used for almost all sounds is the standard propriety Sony Atrac 3 format
    * It's theorized that there were some customizations made in engine by the developer but those are broken in the decompiled code
        * My personal theory: they may have modified it with direct assembly code that Ghidra just can't parse
    * How audio is embedded in Game archives is heavily dependent on the format and System calling the Audio Asset

---
