# More technical details of AFLnet fuzzer in the git repository
<https://github.com/profuzzbench/aflnet>

- **docs/INSTALL**

	4) Linux or *BSD on non-x86 systems

	
	Standard build will fail on non-x86 systems, but you should be able to leverage two other options:

  - The LLVM mode (see llvm_mode/README.llvm), which does not rely on x86-specific assembly shims. It's fast and robust, but requires a complete installation of clang.

  - The QEMU mode (see qemu_mode/README.qemu), which can be also used for     fuzzing cross-platform binaries. It's slower and more fragile, but can be used even when you don't have the source for the tested app.

	If you're not sure what you need, you need the LLVM mode. To get it, try:

	$ AFL_NO_X86=1 gmake && gmake -C llvm_mode

	...and compile your target program with afl-clang-fast or afl-clang-fast++
	instead of the traditional afl-gcc or afl-clang wrappers.

-----------------------
- **docs/QuickStartGuide**
number 3, 4, 5

---------------------------
- **docs/env_variables.txt**
More options/flags for the compiler afl-clang, afl-gcc and afl-clang-fast
and for afl-fuzz itself.

------------------------------
- **docs/historical_notes.txt**
more explanation of afl compare to other tools or techniques

-------------------------------
- **docs/life_pro_tips.txt**
some quick tips of all the files

such as:::

- Need to monitor AFL jobs programmatically? Check out the fuzzer_stats file in the AFL output dir or try afl-whatsup.

- Not sure if a crash is exploitable? AFL can help you figure it out. Specify -C to enable the peruvian were-rabbit mode.

	<https://lcamtuf.blogspot.com/2014/11/afl-fuzz-crash-exploration-mode.html?_sm_au_=iVVNtHn8j7PJMT17J6F3jKH7c2fV2>

"you take a crashing test case and give it to afl-fuzz as a starting point for the automated run. The fuzzer then uses its usual feedback mechanisms and genetic algorithms to see how far it can get within the instrumented codebase while still keeping the program in the crashing state. Mutations that stop the crash from happening are thrown away; so are the ones that do not alter the execution path in any appreciable way. The occasional mutation that makes the crash happen in a subtly different way will be kept and used to seed subsequent fuzzing rounds later on."

-----------------------
- **docs/parallel_fuzzing.txt**
	- Single-system parallelization
	- Multi-system parallelization

-----------------------------
- **docs/perf_tips.txt**
Performance tips

--------------------------
- **docs/siste_projects.txt**
This doc lists some of the projects that are inspired by, derived from, designed for, or meant to integrate with AFL.

	E.g:
	AFL for GCJ Java and other GCC frontends:
	GCC Java programs are actually supported out of the box - simply rename afl-gcc to afl-gcj. Unfortunately, by default, unhandled exceptions in GCJ do not result in abort() being called, so you will need to manually add a top-level exception handler that exits with SIGABRT or something equivalent.

