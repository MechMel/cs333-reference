# Add a System Call
This document describes how to create a system call.
### Manipulated Files
- `user.h`
- `usys.S`
- `syscall.h`
- `syscall.c`
- `sysproc.c`
- `defs.h`
- `runoff.list`
### Definitions
- `CS333_P#` is the flag for your current project. The `#` should be replaced with the number of your current project.
- `nameofsyscall` is the name of your new system call function. It should be short and all lowercase with no hyphens, underscores, or spaces.
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
3. At the bottom of `syscall.h`, below `// student system calls begin here. Follow the existing pattern.` add
```
#define SYS_nameofsyscall    SYS_nameoftheabovesyscall+1
```
4. In the `syscall.c` file find the following list
```
extern int sys_chdir(void);
extern int sys_close(void);
...
extern int sys_uptime(void);
#ifdef PDX_XV6
extern int sys_halt(void);
#endif // PDX_XV6
```
and add the following below `#endif // PDX_XV6`
```
#ifdef CS333_P#
extern int sys_nameofsyscall(void);
#endif // CS333_P#
```
5. In the `syscall.c` file find the following table
```
static int (*syscalls[])(void) = {
[SYS_fork]    sys_fork,
[SYS_exit]    sys_exit,
...
[SYS_close]   sys_close,
#ifdef PDX_XV6
[SYS_halt]    sys_halt,
#endif // PDX_XV6
```
and add the following below `#endif // PDX_XV6`
```
#ifdef CS333_P#
[SYS_nameofsyscall]    sys_nameofsyscall,
#endif // CS333_P#
```
6. In the `syscall.c` file find the following table
```
static char *syscallnames[] = {
  [SYS_fork]    "fork",
  [SYS_exit]    "exit",
...
  [SYS_close]   "close",
#ifdef PDX_XV6
  [SYS_halt]    "halt",
#endif // PDX_XV6
```
and add the following below `#endif // PDX_XV6`
```
#ifdef CS333_P#
  [SYS_nameofsyscall]    "nameofsyscall",
#endif // CS333_P#
```
7. Do only one of the following
    1. If your actual system call code is going to exclusively exist in `sysproc.c` then do the following
        1. In the `sysproc.c` file at the bottom add
       ```
       #ifdef CS333_P#
       int
       sys_nameofsyscall(void)
        {
          // TODO: Impliment your system call here
          return -1;
        }
        #endif // CS333_P#
        ```
    2. If your actual system call code is going to exist somewhere other than in `sysproc.c` then do the following
        1. Create a file for your system call implementation named `nameofsyscall.c` and add the following code to it
        ```
        #ifdef CS333_P#
        int
        nameofsyscall(void or params)
        {
          // TODO: Impliment your system call here
          return -1;
        }
        #endif // CS333_P#
        ```
        2. In the `sysproc.c` file at the bottom add
        ```
        #ifdef CS333_P#
        int
        sys_nameofsyscall(void)
        {
          return nameofsyscall();
        }
        #endif // CS333_P#
        ```
        3. At the botom of the `defs.h` file add
        ```
        #ifdef CS333_P#
        // nameofsyscall.c
        int            nameofsyscall(void or params);
        #endif // CS333_P#
        ```
8. Add any additionaly files you create to the bottom of the `runoff.list` file at the the bottom of the `# Portland State` section like so
```
nameofsomeheaderfileyouadded.h
nameofsomecfileyouadded.c
etc...
```
