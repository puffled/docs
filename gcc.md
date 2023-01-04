### GCC optimization options

this exists because [optimize options](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html) is outdated

the following is from [gcc/opts.cc](https://github.com/gcc-mirror/gcc/blob/master/gcc/opts.cc#L562-L698)

GCC uses four variables internally to decide what to do with the provided `-O` option, `opts->x_optimize`,
`opts->x_optimize_size`, `opts->x_optimize_fast`, and `opts->x_optimize_debug`. unless specified, the
variables are set to zero

 - `-O0`, `-O1`, `-O2`, `-O3`, sets `opts->x_optimize` to the value provided, respectively
 - `-Os` sets `opts->x_optimize` to `2`, and `opts->x_optimize_size` to `1`
 - `-Oz` sets `opts->x_optimize` to `2`, and `opts->x_optimize_size` to `2`
 - `-Ofast` sets `opts->x_optimize` to `3`, and `opts->x_optimize_fast` to `1`
 - `-Og` sets `opts->x_optimize` to `1`, and `opts->x_optimize_debug` to `1`

in other words...

 - `-Os` and `-Oz` imply `-O2`
 - `-Ofast` implies `-O3`
 - `-Og` implies `-O1`

### `-O1`, `-Og`, and above

```
-fcombine-stack-adjustments
-fcompare-elim
-fcprop-registers
-fdefer-pop
-fforward-propagate
-fguess-branch-probability
-fipa-profile
-fipa-pure-const
-fipa-reference
-fipa-reference-addressable
-fmerge-constants
-fomit-frame-pointer
-freorder-blocks
-fshrink-wrap
-fsplit-wide-types
-fthread-jumps
-ftree-builtin-call-dce
-ftree-ccp
-ftree-ch
-ftree-coalesce-vars
-ftree-copy-prop
-ftree-dce
-ftree-dominator-opts
-ftree-fre
-ftree-sink
-ftree-slsr
-ftree-ter
-fvar-tracking
```

### `-O1`, and above

```
-fbranch-count-reg
-fdelayed-branch (if delay slots are enabled)
-fdse
-fif-conversion
-fif-conversion2
-finline-functions-called-once
-fmove-loop-invariants
-fmove-loop-stores
-fssa-phiopt
-fipa-modref
-ftree-bit-ccp
-ftree-dse
-ftree-pta
-ftree-sra
```

### `-O2`, `-Os`, and above

```
-fcaller-saves
-fcode-hoisting
-fcrossjumping
-fcse-follow-jumps
-fdevirtualize
-fdevirtualize-speculatively
-fexpensive-optimizations
-fgcse
-fhoist-adjacent-loads
-findirect-inlining
-finline-small-functions
-fipa-bit-cp
-fipa-cp
-fipa-icf
-fipa-ra
-fipa-sra
-fipa-vrp
-fisolate-erroneous-paths-dereference
-flra-remat
-foptimize-sibling-calls
-fpartial-inlining
-fpeephole2
-freorder-functions
-frerun-cse-after-loop
-fschedule-insns2
-fstrict-aliasing
-fstore-merging
-ftree-pre
-ftree-switch-conversion
-ftree-tail-merge
-ftree-vrp
-fvect-cost-model=very-cheap,
-finline-functions
-ftree-loop-distribute-patterns
```

### `-O2` and above (not `-Os`, and `-Og`).

mostly enables alignment of items, which will improve CPU read/write times (to memory), and possibly increase binary size slightly,
as it has to emit padding data to align them

```
-falign-functions
-falign-jumps
-falign-labels
-falign-loops
-foptimize-strlen
-freorder-blocks-algorithm=stc
-ftree-loop-vectorize
-ftree-slp-vectorize
-fopenmp-target-simd-clone=nohost
-fschedule-insns (if insn scheduling is enabled)
```

### `-O3` and above

mostly enables agressive inlining and loop unrolling, which will fold multiple functions into larger ones, and reduce
iterations of loops at the expanse of repeating loop bodies

```
-fgcse-after-reload
-fipa-cp-clone
-floop-interchange
-floop-unroll-and-jam
-fpeel-loops
-fpredictive-commoning
-fsplit-loops
-fsplit-paths
-ftree-loop-distribution
-ftree-partial-pre
-funswitch-loops
-fvect-cost-model=dynamic
-fversion-loops-for-strides
--param max-inline-insns-auto=30
--param early-inlining-insns-14
--param inline-heuristics-hint-percent=600
--param inline-min-speedup=15
--param max-inline-insns-single=200
```

### `-Ofast`

disregards current C standards compliance, mostly affects fp (floating point) math

allow data races, assume finite fp values, assume no exceptions occur from fp arithmetic, may cause loss of precision
with questionable code (`x * x * x * x * x * x` vs `powf(6, x)`)

```
-ffast-math
-fallow-store-data-races
-fno-semantic-interposition
```
