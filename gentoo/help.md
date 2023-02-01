### gcc, clang, llvm, rust, chromium failed to compile!?

most of the time, you simply ran out of memory, so the compiler processes were killed.

you may verify this via the command `dmesg` or in build logs

gcc will output similar to

```
{standard input}: Assembler messages:
{standard input}:1234: Warning: end of file not at end of a line; newline inserted
{standard input}:1234: Error: unknown pseudo-op: `.l38'
{standard input}: Error: open CFI at the end of file; missing .cfi_endproc directive
gcc: Internal error: Killed (program cc1)
```

the assembler messages have nothing to do with cflags or abything, it is only due to the
subprocess (`cc1`) being terminated, so the code is now missing parts.

(todo the rest of the packages' logs to look for)

the general solution to this, is to reduce your jobs (see [`MAKEOPTS`](https://wiki.gentoo.org/wiki/MAKEOPTS). [zram](https://wiki.gentoo.org/wiki/Zram), [zswap](https://wiki.gentoo.org/wiki/Zswap) or regular swap can help
prevent memory exhaustion.

be aware that compiler processes may use approximately jobs * 2.5 gb for larger packages.
