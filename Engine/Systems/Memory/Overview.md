# Memory Management Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is a general overview of the Memory Management System.

* Purpose: Manage the limited Memory resources for all other Systems so that the game can run smoothly and play without long load times.
* Real Life Counterpart: Accountant
* Notes:
    * Regions will be documented within individual Systems
    * Due to hardcoded allocations in both the Binary and Data on disc:
        * several Systems can be deducted in the Binary based on specific allocations alone and will be noted in those Systems
        * until a new engine is built, all modded game assets must be exact size and structure of asset they replace with only specific contents being different
    * Asset parsing is also Format-specific with hardcoded individual sections of Data on disc being manipulated to form the keys to decompressing and decrypting
        * Currently unknown if file size is related to this aspect of some Formats
        * At least one Format known to use file size as a part of its Magic Number (Format Identifier)

---
