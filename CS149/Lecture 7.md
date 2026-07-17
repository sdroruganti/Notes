

| Resource              | Main operation                                                              | Programmabilit                |
| --------------------- | --------------------------------------------------------------------------- | ----------------------------- |
| CUDA core             | Ordinary per thread FP32/INT arithmetic                                     | General purpose               |
| Tensor core           | Matrix multiply accumulate                                                  | Specialized matrix operations |
| RT core               | Boundary volume hierarchy traversal and ray geometry intersection           | Specialized ray tracing       |
| Load/store unit       | Memory addressing and transfers                                             | Specialized memory operations |
| Special-function unit | Functions such as reciprocal, square root and transcendental approximations | Specialized math              |
