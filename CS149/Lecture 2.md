## What is a computer program?
Ans: It is a list of processor instructions

## What does a processor do?
Ans: A hardware device that modifies state ie. registers and main memory
![[Pasted image 20260706183823.png|697]]

**Superscalar execution**: processor automatically finds independent instructions in an instruction sequence and can execute them in parallel on multiple execution units.

## What is memory?
Ans: An array of bytes:

| Address      | Value at each address |
| ------------ | --------------------- |
| 64 or 32 bit | 1 byte                |

## Cache
Cache is on-chip storage that maintains a copy of a subset of the values in memory. Thereby it is a hardware implementation detail that does not impact the output a program, only its performance
## Cache Line
A **cache line** is the fixed-size chunk of memory that gets moved between memory and cache levels. On most modern x86 CPUs, a cache line is usually **64 bytes**. Cache operate at the granularity of "cache lines". In the figure, the cache:
- Has a capacity of 2 lines
- Each line holds 4 bytes of data
![[Pasted image 20260706185848.png]]

## Fetch and Decode

Fetch and decode are the first stages of running instructions on a CPU. **Fetch** means the CPU gets the next instruction bytes from memory/cache. **Decode** means the CPU figures out what the instruction bytes mean by translating instruction bytes into CPU operations.

### Fetch
Get:
```
RIP
```
Got:
```
RIP = 0x401000
```

### Decode
Instruction:
```
add rax, rbx
```
Decoder translates that into:
```
Read rax
Read rbx
Send values to ALU
Add them
Write result back to rax
```
## Add execution units (ALUs) to increase compute capability
**SIMD processing**: single instruction, multiple data

In SIMD execution, a single instruction is broadcast across multiple vector lanes, allowing the same operation to run in parallel on multiple data elements.
![[Pasted image 20260706194527.png]]![[Pasted image 20260706194238.png]]


## Coherent execution
- Property of a program where the same instruction sequence applies to many data elements
- Coherent execution **IS NECESSARY** for SIMD processing resources to be used efficiently
- Coherent execution **IS NOT NECESSARY** for efficient parallelization across different cores, since each core has the capability to fetch/decode a different instructions from their thread's instruction stream
## Divergent execution
- A lack of instruction stream coherence in a program
## Different parallelization techniques

**Superscalar**: multiple instructions per cycle inside one core
**SIMD**: one instruction operates on multiple data elements
**Multithreading**: multiple threads share/occupy CPU execution resources
**Multicore**: multiple independent CPU cores on one chip

### Superscalar
![[Pasted image 20260706202603.png|314]]
## SIMD
![[Pasted image 20260706203206.png|316]]
## Multi-threading
![[Pasted image 20260706203716.png]]
## Multi-core
![[Pasted image 20260706202642.png]]