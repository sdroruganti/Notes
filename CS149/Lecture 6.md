## Arithmetic intensity

$$
\frac{\text{Amount of computation, e.g., instructions}}
     {\text{Amount of communication, e.g., bytes}}
$$
- If numerator is the execution time of computation, ratio gives average bandwidth requirement of code.
- 1/**"Arithmetic intensity"** = communication-to-computation ratio
	- Some people like to refer to communication to computation ratio
- High arithmetic intensity (low communication-to-computation ratio) is required to efficiently utilize modern parallel processors since the ratio of compute capability to available bandwidth is high

## Reducing communication costs

### Amortize communication overhead

- Send fewer messages.
- Make each message larger.
- Coalesce many small transfers into one bulk transfer.

### Reduce communication latency

- Improve locality.
- Place communicating work closer together.
- Improve the underlying memory or network architecture.

### Reduce contention

- Replicate heavily accessed resources.
- Use local copies or distributed queues.
- Use finer-grained locks.
- Stagger accesses so every worker does not request the resource simultaneously.

### Overlap communication and computation

- Use asynchronous communication.
- Perform independent work while a transfer is in progress.
- Hardware may help through:
  - pipelining,
  - multithreading,
  - prefetching,
  - out-of-order execution.

- Overlap requires enough independent work to execute while communication is pending.
## Roofline model

The roofline model estimates the maximum performance obtainable at a given
arithmetic intensity.

$$
\text{Attainable performance}
\leq
\min\left(
\text{Peak compute throughput},
\text{Memory bandwidth} \times \text{Arithmetic intensity}
\right)
$$

### Diagonal region

- Memory-bandwidth-bound.
- Increasing arithmetic intensity can improve performance.
- Useful optimizations include:
  - blocking,
  - loop fusion,
  - data reuse,
  - reducing memory traffic.

### Horizontal region

- Compute-bound.
- Memory bandwidth is no longer the dominant limit.
- Increasing arithmetic intensity alone will not improve performance.
- Useful optimizations include:
  - SIMD/vectorization,
  - instruction-level parallelism,
  - reducing instruction count,
  - improving execution-unit utilization.

### Ridge point

The transition between memory-bound and compute-bound execution occurs near:

$$
\text{Ridge-point intensity}
=
\frac{\text{Peak compute throughput}}
     {\text{Peak memory bandwidth}}
$$
![[Pasted image 20260714214855.png]]

![[Pasted image 20260714214915.png]]