# Production Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a  general overview of the entire Asset Production Stack. For more specific information on each individual part of it, such as Asset storage or how each System handles Production, those will be in separate sections of the System documentation.

* Purpose: General purpose shared Production stack.
* Customers:
    * Battle System
    * Field System
* Real World Counterpart: Multi-Industry Corporation with full control of the entire Production line
* Pipeline:
    * Load Orchestration Header
    * Determine which Production stack to use based on which System requested Asset and Type of Orchestrator
    * Parse Scripting structure for Instructions and Implementation
    * Cross-Reference with a Generic Data Table in the Game's Binary
    * Pass all of this to the Orchestrator
    * Wait for next Production request
---
