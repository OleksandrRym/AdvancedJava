# HotSpot

## Basic JVM

![](assetss/HotSpotAnatomy.png)

- ### Interpret - executes byte code instruction by instruction
- ### Profile - store and collect statistic
- ### JustInTime - convert hot methods to machine code
- ### deoptimize ( optional ) - deoptimize code

---
# JIT
- compiler which detect hot methods and convert it to machine code
- on the hood use c1 and c2 workers
---
## c1 c2
### Separate threads which process optimizations. Work **ASYNC** get tasks from queue , process and compile it
 
- c1 (1-3) - for fast start (client)
- c2 (4) - for server projects (server)

## Tiered levels

--- 
- 1 - Simple:
    - very fast compilation
    - target: quickly exit interpretation phase
- 2 - Limited profiling:
    - collects some profile info for better optimizations
- 3 - Full profiling:
    - uses full profiling of trivial methods and hot branches
    - prepares accurate data for C2 optimizations
  
    
- 4 - Highly optimized:
    - performs deep, aggressive optimizations
      (inlining, loop unrolling, escape analysis, devirtualization)
    - target: maximum throughput for long-running server methods
--- 
## Inlining Optimizations
- ### When we call method(A) inside method(B) in body (B) we recive body (A)

![](assetss/inliningInPractice.png)

---

## Code cache
### Place in JVM when c-workers stored machine code
- Code Cache — heap-like structure for binary code.
- Free List: linked-list free blocks ( when JIT create new method , he find space in list)
- Method Objects: binary code + metadata ( inlining, instructions , const and etc)
### NoN Heap - have own limit of pool
### Sweeper - clean code cache ( NOT GC )
- Alive: Method active used
- Not Entrant: method do invalidate , but old thread can execute this code ( by deoptimizer)
- Zombie: Sweeper check all threads - and 0 threads use it ( so, this code stay in memory - but unused)
- Inactive (Reclaimed): Sweeper remove method, and free space go to Free-list
![](assetss/HSA+CC.png)
