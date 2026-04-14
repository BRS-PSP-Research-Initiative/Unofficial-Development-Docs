# HP Failsafe Findings Documentation

---

*Copyright 2026 - Brad D*
*In collaboration with Akuzakun who discovered it initially through exploring a known Defender Glitch; the time time and date will be in relation to his tests*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Date Found: Unknown; Defender Glitch was known but no records available of when it was first discovered along with no previous tests or videos found
* Date Tested: 04/10/2026
* Time: 8:00 AM CST
* Regions Affected: jpn, usa, eur
* Description: During exploration of what the Defender Glitch could be used for, it was discovered that if a fight ended with Stella at 0 HP while Defender was used and held, instead of receiving a Game Over, she would transition to the next Phase (in Boss fights) or the Stage (Field) with 1 HP left.

---

## Exploit code Snippets:
* No Exploit path found yet

---

## Unique Discoveries:
* All Skills can trigger a Zombie State (still alive when HP is 0 until the end of the Skill Animation or the Player stops holding the Input required to helm it)
* The Minimap tracks the HP of all Combatants on the Map
* Playable Characters (PC) with HP that are tracked in code by ID:
    * Stella - 0
    * Zig - 1
    * Unknown Third PC - 3
* Bosses may be tracked as ID 4-7 with their weapons tracked as in range 0x4fd1, 0x4fd2, and 0x4fdb - 0x4fe2
* Other Combatants are tracked in groups of 2 from 0x4fd3 - 0x4fda
* In Combat, these are unique values for the PCs:
    * Stella - 0x2711
    * ZIG - 0x2712
    * Unknown - 0x2714
* This one is unique to the Rendering System:
    * Debug Camera? - 0x12c
* PC HP can possibly be Negative Buffer Overflowed but the amount of time required would make it not worth it without another exploit found that would disable the failsafe entirely
    * Failsafe code Snippet:
     ```
    health = (uint)((*(uint *)(id + ((int)hp >> 5) * 4 + 0x80) & 1 << (hp & 0x1f)) != 0);
    ```

---
