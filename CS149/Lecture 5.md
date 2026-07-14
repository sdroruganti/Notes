## Amdahl's Law

Amdahl's law explains the maximum speedup you can get by parallelizing a program. If a part of your program must run serially, the adding more CPU cores /GPUs cannot make that serial part faster.

Formula:

```
Speed up = 1/((1 - P) + P / N)
```

```
P = Parallelizable fraction of the program
N = Number of processors/cores
(1 - P) = Serial fraction of the program
```

## CPU Parallelism

OpenMP, Cilk, and Pthreads allow for the user to spawn multiple threads to compute tasks. Mental model for each:

|         | Abstraction level | Use case                                      | Thread management                          |
| ------- | ----------------- | --------------------------------------------- | ------------------------------------------ |
| OpenMP  | High              | Parallel loops                                | Runtime manages threads                    |
| Cilk    | High              | Recursive loops                               | Runtime manages workers, and work stealing |
| Pthread | Low               | Individual resource allocation and definition | User manages everything                    |

## OpenMP

OpenMP is best for parallelizing structured code, especially loops, with high abstraction.

```
#pragma omp prallel for
for (int i = 0; i < n; ++i){
	output[i] = foo(input[i])
}
```

The OpenMP runtime:
- Creates or reuses a thread pool.
- Divides loop iterations among threads.
- Synchronizes threads at the end of the loop.
- Provides locks, reductions, tasks, barriers, and scheduling policies

## Cilk

Cilk is designed primarily for task parallelism, especially recursive algorithms like quick sort. Cilk uses **work stealing**. Each worker maintains a task queue and an idle worker steals work from another worker. Cilk gives less direct control that pthreads, but its scheduler automatically balances irregular workloads.

```
cilk_spawn foo();
bar();
cilk_sync;
```

In the above program:
1. `foo()` may execute concurrently with `bar()`.
2. `cilk_sync` waits until the spawned child task complete.

## Pthreads

POSIX threads provide direct, low-level thread control.

```
pthread_t thread;
pthread_create(&thread, NULL, foo, NULL);
bar();
pthread_join(thread, NULL);
```

You manage the following:
- Thread creation and destruction
- Arguments and return values
- Mutexes (for race conditions)
- Condition variables
- Barriers
- Thread joining
- Shared-memory synchronization