# test-coverage

Repository for tools to analyse functional test coverage of applications.

One of the proposed method is to use syscalls as a metric. The syscall profile is then compared to a one dynamically generated when running functional tests for the same application executable.

The `analyze.sh` statically analyses an ELF binary by disassembling and building a syscall list with a similar fashion as strace does, including syscall name and arguments.

The only application type supported are ones compiled. Script and application that use interpreted languages are not supported by this method.

## `analyze`

```shell
analyze EXECUTABLE
```

