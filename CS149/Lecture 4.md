## SPMD programming abstraction
- Call to ISPC function spawns "gang" of ISPC "program instances"
- All instances run ISPC code concurrently
- Each instance has its own copy of local variables
- Upon return, all instances have complete

Gang size is set during the compile time where the user sets it
## ISPC language keywords
- **programCount**: number of simultaneously executing instances in the gang (uniform value)
- **programIndex**: id of the current instance in the gang (a non-uniform value: "varying")
- **uniform**: A type modifier. All instances have the same value for this variable. Its use is purely an optimization. Not needed for correctness.