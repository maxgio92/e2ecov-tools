# e2ecov-tools

Repository for tools to analyse end-to-end functional test coverage of applications.

One of the proposed method is to use syscalls as a metric. The syscall profile is then compared to a one dynamically generated when running functional tests for the same application executable.

The `analyze.sh` statically analyses an ELF binary by disassembling and building a syscall list with a similar fashion as strace does, including syscall name and arguments.

The only application type supported are ones compiled. Script and application that use interpreted languages are not supported by this method.

## `analyze`

Analyse analyzes and reports the system calls the binary executable executes.

### Requirements
- binutils (`objdump` tool)

```shell
analyze EXECUTABLE
```

For example:

```shell
$ analyze myapp
openat
read
gettid
getpid
gettid
tgkill
getpid
kill
getpid
tgkill
setitimer
timer_create
timer_settime
timer_delete
mincore
clock_gettime
rt_sigprocmask
rt_sigaction
mmap
munmap
madvise
futex
clone
gettid
exit
sigaltstack
arch_prctl
sched_yield
sched_getaffinity
clock_gettime
```

### Limitations

There are natural limitations on the static analysis this command does of syscall parameters, due to the nature of the stack and the architecture-specific calling conventions.

Furthermore, some language compilers embeds the runtime into the binary, like Go does. Consequently it requires to filter out runtime's sycalls.
