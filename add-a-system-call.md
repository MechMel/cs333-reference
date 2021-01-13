# Add a System Call
1. In `user.h` at the bottom of `// system calls` add
```
#ifdef CS333_P1
int nameofsyscall(void or params);
#endif // CS333_P1
```
