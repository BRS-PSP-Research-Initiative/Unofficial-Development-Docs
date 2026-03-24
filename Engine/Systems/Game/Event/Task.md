# Event Task subSystem Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a general overview of the Event Task sub-System.

* Purpose: Handles performing actions related to System requests in an ordered fashion.
* Real Life Counterpart: Task Master
* Notes:
    * Relies on a Global Callback mechanism that does the following:
        1. Stores a clean copy of previous Task Callback Heap
        2. Allocates Heap of an unspecified size
        3. If heap is empty, do nothing; otherwise continue
        4. Populate Heap with default start values and Start Position, Address of Heap, and optional Pointer Label + Continue Status and Completed Tasks this session
        5. If a Start Position is set, adjust Heap based on offsets 0x4c and 0x50
        6. Replace previous Task Callback Heap with local Heap
        7. Add local Heap to Task Table
        8. Update Heap with any Subcontexts given
        9. Increase Task Callback Queue count by 1
        10. Copy Local Heap to a Second Local Heap
        11. If Task Callback Queue is not empty, populate Local Heap with Queued Task Data and update Second Local Heap updated Task Callback Pointer
        12. Set Task Callback Pointer to Second Local Heap
        13. Return Local Heap to Callback caller
    * Can work in conjuction with Scripting System if System requestor uses it to modify Context / Subcontext
        * NOTE: This can complicate things fast since at least two Systems have different flavors of Scripting Implementation
    * If a System has a Watching mechanism (wait and see if a certain memory region is modified), this Subsystem can also be a Messaging System, especially if it is watching the Task Callback Queue data

---
