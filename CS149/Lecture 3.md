
![[Pasted image 20260707192543.png]]

A **scalar ALU op** works on one value at a time.
A **vector ALU op** works on multiple values at the same time.
## Scalar ALU operation
Scalar means single value. Example:
```
add rax, rbx
```
This means:
```
rax = rax + rbx
```
One operation. One pair of values. One result

## Vector ALU operation
Vector mean multiple values packed together. Example:
```
A = [1, 2, 3, 4]
B = [10, 20, 30, 40]
```
A vector add does:
```
A + B = [11, 22, 33, 44]
```
Mental model:
```
Vector ALU / SIMD unit

lane 0:  1 + 10  ──> 11
lane 1:  2 + 20  ──> 22
lane 2:  3 + 30  ──> 33
lane 3:  4 + 40  ──> 44
```
## In modern computing, bandwidth is the ==critical== resource

Performant parallel programs will:
- Organize computation to fetch data from memory less often
	- Temporal locality optimizations: Reuse data previously loaded by the same thread
	- Inter-thread cooperation: Share data across threads
- Favor performing additional arithmetic to storing/reloading values (the math is "**free**")
- Main point: programs must access memory infrequently to utilize modern processors efficiently