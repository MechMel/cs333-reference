# Add a System Call
This document describes how to create a system call.
### Manipulated Files
- `user.h`
- `usys.S`
- `syscall.c`
### How to Read This
- `CS333_P#` is the flag for your current project. The `#` should be replaced with the number of your current project.
- `nameofsyscall` is the name of your new system call function. It should be short and all lowercase with no hyphens, underscores, or spaces.
- 
### Steps
1. In `user.h` at the bottom of `// system calls` add
```
#ifdef CS333_P#
int nameofsyscall(void or params);
#endif // CS333_P#
```
2. At the bottom of `usys.S` add
```
SYSCALL(nameofsyscall)
```
3. At the bottom of `syscall.c`, below `// student system calls begin here. Follow the existing pattern.` add
```
#define SYS_nameofsyscall    SYS_nameoftheabovesyscall+1
```
