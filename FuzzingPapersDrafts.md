# Fuzzing Papers Drafts

**_Fuzzing_** is a software-testing technique that detects vulnerabilities by executing target programs with a large amount of abnormal or random test cases.

**Table of Contents**

[TOCM]

[TOC]

# [Active Fuzzing for Testing and Securing Cyber-Physical Systems](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#active-fuzzing-for-testing-and-securing-cyber-physical-systems)
# [UNIFUZZ: A Holistic and Pragmatic Metrics-Driven Platform for Evaluating Fuzzers](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#unifuzz-a-holistic-and-pragmatic-metrics-driven-platform-for-evaluating-fuzzers)
# [HFL: Hybrid Fuzzing on the Linux Kernel](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#hfl-hybrid-fuzzing-on-the-linux-kernel)
# [CSEFuzz: Fuzz Testing Based on Symbolic Execution](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#csefuzz-fuzz-testing-based-on-symbolic-execution)
# [V-Fuzz: Vulnerability-Oriented Evolutionary Fuzzing](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#v-fuzz-vulnerability-oriented-evolutionary-fuzzing)
# [Fuzzing Symbolic Expressions](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#fuzzing-symbolic-expressions)
# [DIFFUZZ: Differential Fuzzing for Side-Channel Analysis](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#diffuzz-differential-fuzzing-for-side-channel-analysis)
# [FUZZIFICATION: Anti-Fuzzing Techniques](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#fuzzification-anti-fuzzing-techniques)
# [FUDGE: Fuzz Driver Generation at Scale](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#fudge-fuzz-driver-generation-at-scale)
# [FuzzGen: Automatic Fuzzer Generation](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#fuzzgen-automatic-fuzzer-generation)
# [ParmeSan: Sanitizer-guided Greybox Fuzzing](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#parmesan-sanitizer-guided-greybox-fuzzing)
# [USBFuzz: A Framework for Fuzzing USB Drivers by Device Emulation](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#usbfuzz-a-framework-for-fuzzing-usb-drivers-by-device-emulation)
# [MOPT: Optimize Mutation Scheduling for Fuzzers](https://github.com/pinkhat-m/Internship2021/blob/master/FuzzingPapersDrafts.md#mopt-optimize-mutation-scheduling-for-fuzzers)


## Active Fuzzing for Testing and Securing Cyber-Physical Systems
<https://arxiv.org/pdf/2005.14124.pdf>

##### **Active fuzzing** -> an automatic approach for finding test suites of packet-level
CPS network attacks, targeting scenarios in which training data is limited, and in which attackers can observe sensors and manipulate packets.

Steps:


1) First, data is collected: packets are sniffed from the network, their payloads are extracted, and (true) sensor readings are queried.
2) Second, we pre-train initial regression models, that take concatenations of packet payloads and predict the future effects on given sensors.
3) Third, we apply an online active learning framework, iteratively improving the current model by sampling payloads estimated to maximally improve it.
4) Finally, we search for candidate attacks by flipping important bits in packet payloads, and using our learnt models to identify which of them will drive the system to a targeted unsafe state.

Active fuzzing is effective at discovering:

- Packet-level flow
- Pressure
- Over/underflow attacks
- Achieving comparable coverage to an established benchmark
- An LSTM-based fuzzer

but with substantially less training time, data, and network access.

## UNIFUZZ: A Holistic and Pragmatic Metrics-Driven Platform for Evaluating Fuzzers
<https://arxiv.org/pdf/2010.01785.pdf>

#### **Evaluation**

###### - Usability Issues of Existing Fuzzers
Whether the existing implementation of fuzzers works in practice.

**First**, some fuzzers may be difficult or complicated to be used directly.

**Second**, we find that there are numerous flaws (e.g., incorrect judgment on crash, abnormal behaviors during the fuzzing process) with the implementation of many fuzzers, which may cause negative impacts on their performance.

###### - Lack of Pragmatic Real-World Benchmark Programs
**First**, they should have similar features as the real-world programs --->>> including coding styles, sizes and vulnerabilities.

**Second**, benchmark programs should exhibit a diversity of functionalities, sizes, vulnerability types.

**Third**,each benchmark program should contain at least one vulnerability(bug) that can be found within a reasonable amount of time.

**Fourth**, the benchmark programs should be easy to use (users can easily use the benchmark programs and get the evaluation results.)

###### - Lack of Proper and Comprehensive Performance Metrics
A collection of performance metrics in six categories:
- Quantity of unique bugs
- Quality of bugs
- Speed of finding bugs
- Stability of finding bugs
- Coverage
- Overhead.


## HFL: Hybrid Fuzzing on the Linux Kernel
<https://wcventure.github.io/FuzzingPaper/Paper/NDSS20_HFL.pdf>

**Symbolic Execution** is a program testing technique that can generate an input that drives the target program’s execution to a certain program path. To do this, symbolic execution takes all input to the target program as symbols and keeps tracking the program’s runtime context as symbolic expressions.

- limitation in handling a tight branch condition:
  - Fuzzing-> because of random testing cannot find
  - Symbolic execution-> encounter state explosion

**Combining symbolic execution and fuzzing**

Advantages:

- Finding unknown vulnerabilities in recent Linux kernels.
- Higher code coverage.
- Regarding vulnerability discovery performance, found known vulnerabilities more than three times faster than Syzkaller.

**Challenges in applying Hybrid Fuzing to kernel**

1) Indirect control transfer determined by input
2) Internal system state requirements
3) Nested argument type inference

**Generic Hybrid Fuzzing Design Features**

1) kernel syscall fuzzing

HFL:

- Indentifying kernel bugs triggered by user program
- Generating or mutating a user program(sequence of system calls)
- constructing or mutating syscalls based on pre-defined syscall templates

Since Linux does not provide a formally defined rule for syscall invocation, thus this template is not only manually defined but also incomplete; therefore, HFL designs fully automated kernel-specific features.

2) coverage-guided fuzzing
- HFL instruments all code blocks in the kernel.
- Collect execution coverage information when executing a program.
- Based on those information, HFL determines whether a new input assists to augment the execution coverage.
- HFL keeps track of all code blocks.
- Checks if the new input executes any uncovered block. If so, HFL pushes the new input into a corpus

3) symbolic analysis.

Fuzzer’s well-known limitation is that it cannot drive an execution passing through a hard constraint imposed in some branch conditions. Hybrid fuzzing techniques, which typically combines symbolic execution to solve such hard constraints.


## CSEFuzz: Fuzz Testing Based on Symbolic Execution
<https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9222017>

To address the problem of quality of the initial seed test cases which influences the code coverage and defect detection capability of fuzz testing, CSEFuzz(Coverage-guided Symbolic Execution for Fuzz testing) is proposed which is a fuzz testing approach based on symbolic execution for defect detection.

**First**, CSEFuzz generates candidate test cases for the program under testing by symbolic execution and collects coverage information of the test cases.

**Then**, CSEFuzz extracts the test-case templates of the test cases and selects a set of test-case templates according to specific coverage criteria such as decision coverage, conditional coverage and path coverage.

**Finally**, CSEFuzz selects test cases according to the selected test-case templates, and the selected test cases are used as initial seed test cases to start fuzz testing.


###### Evaluation by using CSEFuzz tool
1) Symbolic Execution module --> collecting path constraints and using a constraint solver to generate test-case candidates with high path coverage
2) Initial seed test case selection module --> collecting coverage information of those test cases by executing programs dynamically, generating test case templates, selecting initial test cases based on those templates
3) Fuzz testing module --> validating the initial seed test cases, then mutating to generate new test cases

To **evaluate** the influence of selecting initial seed test cases based on different coverage criteria, CSEFuzz implements four different coverage criteria.

- CSEFuzzn(n) --> indicates that no test case selection is performed, and all the test cases are used as seeds directly
- CSEFuzz(d) --> indicates that the initial seed test cases are selected based on decision coverage
- CSEFuzz(c) --> indicates that the initial seed test cases are selected based on condition coverage
- CSEFuzz(p) --> indicates that the initial seed test cases are selected based on path coverage.


## V-Fuzz: Vulnerability-Oriented Evolutionary Fuzzing
<https://wcventure.github.io/FuzzingPaper/Paper/Arxiv19_VFuzz.pdf>

**V-Fuzz** aims to find bugs on binary programs efficiently and quickly in a limited time.

V-Fuzz consists of two main components to improve the fuzzing performance:

- A neural network-based vulnerability prediction model --> the prediction model(built by leveraging machine learning or deep learning techniques) on a given binary program will do analysis on which components of program are more likely to have vulnerabilities.

	Static Vulnerable Score(SVS) will be assign to each basic blocks that are more likely to be vulnerable, so lately fuzzer can generate inputs that are more likely to cover the basic blocks.

- A vulnerability-oriented evolutionary fuzzer --> will leverage the prediction information to generate high-quality inputs which tend to arrive at these potentially vulnerable components.




## Fuzzing Symbolic Expressions
<https://arxiv.org/pdf/2102.06580.pdf>

Fuzzy-SAT takes inspiration from symbolic execution and coverage-baed grey-box fuzzing

FUZZOLIC -> a new hybrid fuzzer based on QEMU

integrating Fuzzy-SAT with QSYM

(Unfortunately, I still cannot get the main idea of this paper)

## DIFFUZZ: Differential Fuzzing for Side-Channel Analysis
<https://wcventure.github.io/FuzzingPaper/Paper/ICSE19_DIFFUZZ.pdf>

**Side-channel attacks** is an attack which an attacker could uncover secret data from the program by observing non-functional characteristics of program behavior with considering resources such as execution time, consumed memory, response size, network traffic, or power consumption.

**Differential fuzzing** is a popular software testing technique that detects bugs by providing the same input to similar applications (or to different implementations of the same application), and observing differences in their execution.

###### **DIFFUZZ**
is a fuzzing-based dynamic analysis approach for detecting side-channel vulnerabilities related to time and space by analyzing two copies of the same program(same public inputs but different secret values) and using **resource-guided heuristics** to find inputs that maximize the difference in resource consumption between secret dependent paths. The methodology of DIFFUZZ can be applied to programs written in any language.	

###### **Analysis Procedure:**:
- User should provide initial seed files
- Also provides a driver(written manually), which parses an input file into three elements:
	- pub (common public value)
	- sec1, and sec2 (two secret values, one for each program copy)
- Driver executes two copies of the program on these inputs
- And measures the cost difference
- The seed files are put into a queue for further processing(as a central data structure)
- There is a fuzzer to take inputs from the queue and mutate them repeatedly
- Then DIFFUZZ executes the driver with those inputs to find if they are interesting for further processing or not, so needs to computes the cost difference between two executions and compares with the maximum cost difference(high-score)
- The inputs that increase the code coverage of the program or increase high-score will be put into the queue for another process, until a user-specified timeout occurs.

###### **Analysis Outcome**

- If the cost difference is **large** --> means that the program has a side-channel vulnerability
	- So a developer can use the provided inputs to fix the vulnerability by making the cost similar on both program paths.
- If the cost difference is **small** (or zero) --> it could mean that the program has no vulnerabilities or that the fuzzer was not run long enough.


## FUZZIFICATION: Anti-Fuzzing Techniques
<https://wcventure.github.io/FuzzingPaper/Paper/USENIX19_FUZZIFICATION.pdf>

**Fuzzification** decreases:
- the number of discovered paths
- the number of identified crashed
- the number of detected bugs

Fuzzification **features**: (it is not practical simultaneously)
- First, it should be effective for hindering existing fuzzing tools, finding fewer bugs within a fixed time;
- second, the protected program should still run efficiently in normal usage;
- third, the protection code should not be easily identified or removed from the protected binary by straightforward analysis techniques.

Attackers also like a trusted party could do the fuzzing method to find the bugs, so we need a technique to avoid this problem. To solve this problem developer compiles the program code in two different versions.

- One is compiled normally to generate a normal binary.
- Another one is compiled with Fuzzification techniques to generate a protected binary.


Then developer distributes the protected binary version to adversary and trusted parties; but they cannot find as many bugs quickly.
On the other hand they distribute the normal binary to trusted parties so normal parties can do the fuzzing test on the normal binary with the native speed and find more bugs.
This approach helps developer to receive bug reports from trusted parties and fix them before attackers abuse it.


## FUDGE: Fuzz Driver Generation at Scale
<https://wcventure.github.io/FuzzingPaper/Paper/FSE19_FUDGE.pdf>

**Fudge** automatically generates fuzz driver candidates for libraries based on existing client code. Fudge generates thousands of new drivers for a wide variety of libraries. Each generated driver includes a synthesized C/C++ program and a corresponding build script, and is automatically analyzed for quality.

Fudge system consists of two main components:
1) A backend pipeline generating fuzz target candidates
	
    The pipeline consists of
    
    - the Slicing module: The Slicer module scans the whole code repository looking for usages of this library, to extract code snippets.
    - Synthesis module: The Synthesis module receives the extracted code snippet and completes it by  ensuring that (1) our target API call is fed with the fuzzer input and (2) there are no UnknownX placeholders left in the code.
    - Evaluation module: Finally, each of these synthesized candidate targets is evaluated by building and running it with a preconfigured time bound.
    
2) A frontend UI exposing these to the user

	A system shows the information produced by the backend candidate generation pipeline.
    - Candidate targets view
    - Packages view
    - APIs view
    - Use sites view
    - Existing targets view

## FuzzGen: Automatic Fuzzer Generation
<https://www.usenix.org/system/files/sec20fall_ispoglou_prepub.pdf>

Developed concurrently and independently from **FuzzGen**, **FUDGE** is the most recent effort on automated fuzz driver generation. FUDGE leverages a single library consumer to
infer valid API usages of a library to synthesize fuzzers. 

There are two major differences:

- First, FUDGE extracts sequences of API calls and their context (called “snippets”) from a single library consumer and then uses these snippets to create fuzz drivers which are then tested using a dynamic analysis.

	Instead of extracting short snippets from consumers, FuzzGen minimizes consumers (iterating over the consumer’s CFG) to only the library calls, their dependent checks, and dependent arguments/data flow.
    
- Second, FUDGE creates many small fuzz drivers from an extracted snippet.

	In comparison, FuzzGen merges multiple consumers to a graph where sequences of arbitrary length can be synthesized.
    
    Instead of the 1-N approach of FUDGE, FuzzGen uses an M-N approach to increase flexibility.
    
    Compared to FUDGE, FuzzGen fuzzers are larger, more generic, focusing on complex API interaction and not just short API sequences.


**FuzzGen** is automatically synthesizing fuzzers for complex libraries in a given environment. FuzzGen leverages a whole system analysis to infer the library’s interface and synthesizes fuzzers specifically for that library. FuzzGen requires no human interaction and can be applied to a wide range of libraries. Furthermore, the generated fuzzers leverage LibFuzzer to achieve better code coverage and expose bugs that reside deep in the library.

FuzzGen consists of three parts:

1) An API inference: The API inference component builds an A<sup>2</sup>DG based on all test cases and programs on a system that use a given library.

2) An A<sup>2</sup>DG construction mechanism: The A<sup>2</sup>DG is a graph that records all API interactions, including parameter value range and possible interactions. Our analysis infers library use and constructs a generic A<sup>2</sup>DG based on this use.

3) A fuzzer generator that leverages the A<sup>2</sup>DG to produce a custom libFuzzer “fuzzer stub”. The fuzzer generator synthesizes fuzzers that build up complex state and leverage fuzz input to trigger faults deep in the library.

## ParmeSan: Sanitizer-guided Greybox Fuzzing
<https://wcventure.github.io/FuzzingPaper/Paper/USENIX20_ParmeSan.pdf>

**Coverage-guided fuzzers** optimize for covering as much code as possible. Since code coverage over-approximates bug coverage, this approach is less than ideal and may lead to non-trivial time-to-exposure (TTE) of bugs.

**Directed fuzzers** try to address this problem by directing the fuzzer to a basic block with a potential vulnerability. This approach can greatly reduce the TTE for a specific bug, but such special-purpose fuzzers can then greatly under-approximate overall bug coverage.

**ParmeSan** is a new sanitizer-guided fuzzer that greatly reduces the TTE of real-world bugs, and finds bugs 37% faster than existing state-of-the-art coverage-based fuzzers (Angora) and 288% faster than directed fuzzers (AFLGo), while still covering the same set of bugs.
1) ParmeSan relies on off-the-shelf sanitizer checks to automatically maximize bug coverage for the target class of bugs.
2) This allows ParmeSan to find bugs such as memory errors more efficiently and with
lower TTE than existing solutions. 
3) Like coverage-guided fuzzers, ParmeSan does not limit itself to specific APIs or areas of the code, but rather aims to find these bugs, wherever they are.
4) Unlike coverage-guided fuzzers, however, it does not do so by blindly covering all basic blocks in the program. Instead, directing the exploration to execution paths that matter — having the greatest chance of triggering bugs in the shortest time.

- Three main **components** of ParmeSan sanitizer-guided fuzzing pipeline:

  1)_Target acquisition_: collects a number of interesting targets that we want our fuzzer to reach. The set of targets is generated by the instrumentation operated by the given sanitizer on the given program. Then, uses pruning heuristics to weed out uninteresting instrumentations for better efficiency.
  
  2)_Dynamic CFG_: can track input-dependent CFG changes and provide feedback to input mutation on which input bytes may affect the CFG for a given input.
  
  3)_Fuzzer_: takes an instrumented binary, the set of targets, and a set of seeds as input. It starts with input seeds to get an initial set of executed basic blocks and the conditions covered by these basic blocks. It then tries to steer the execution towards targets from the target acquisition component using the precise distance information that is provided by the dynamic CFG component.
  
  We use DFA to solve branch constraints. In ParmeSan, this intuition is used not just to find new code to reach the targets efficiently but also to quickly flip the reached target
sanitizer checks and trigger bugs. Finally the output of the fuzzer consists of generated error inputs.

## USBFuzz: A Framework for Fuzzing USB Drivers by Device Emulation
<https://nebelwelt.net/files/20SEC3.pdf>

**USBFuzz** is a cheap, portable, flexible, and modular USB fuzzing framework. At its core, USBFuzz uses an emulated USB device to provide fuzz input to a virtualized kernel. In each iteration, a fuzzer executes a test using the emulated USB device virtually attached to the target system, which forwards the fuzzer generated inputs to the drivers under test when they perform IO operations.

* Different kinds of **attack** could be possible:

	(i) Exhaustive privileges for USB devices (e.g., the famous “autorun” attack that allows USB storage devices to start programs as they are plugged in) ---->>> This attack can be solved by reconfiguring the operating system through customized defenses (e.g., disabling “autorun”, GoodUSB, USBFilter, or USBGuard)
   
    (ii) Electrical attacks leveraging physical design flaws ---->>> Hardware attacks can be protected through improved interface design.
    
    (iii) Exploiting software vulnerabilities in the host OS ---->>> These issues are hard to find and have high security impact. (**_USBFuzz_**)
    
    
* High level functionalities of main **components**:

1) **Fuzzer:** runs as a userspace process on the host OS. 

    (i) mutating the data fed to device drivers in the target kernel;

    (ii) monitoring and controlling test execution.
2) **Guest System:** is a virtual machine that runs a target kernel containing the device drivers to test. It provides support for executing the guest code, emulating the fuzzing device as well as the supporting communication device.
3) **Target Kernel:** contains the code (importantly, device drivers) and runs inside the guest system. The drivers in the kernel are tested when they process the data read from the emulated fuzzing device.
4) **Fuzzing Device:** is an emulated USB device in the guest system which is connected through the emulated USB interface to the guest system. It forwards the fuzzer-generated data to the host when the target kernel performs IO operations on it.
5) **Communication Device:** is an emulated device in the guest system intended to facilitate communication between the guest system and the fuzzer component.
6) **User Mode Agent:** This userspace program runs as a daemon process in the guest system. It monitors the execution of tests. Optionally, it can be customized to perform additional operations on the fuzzing device to trigger function routines of drivers during focused fuzzing.

## MOPT: Optimize Mutation Scheduling for Fuzzers
<https://wcventure.github.io/FuzzingPaper/Paper/USENIX19_MOPT.pdf>

The target of **MOPT** is to find an optimal selection probability distribution of operators by aggregating the probabilities found by the particles. MOPT can quickly converge to the best solution of the probability distribution for selecting mutation operators and thus improves the fuzzing performance significantly(can be applied to a wide range of mutation-based fuzzers).

The **mutation scheduler** aims at choosing the next optimal mutation operator, which could find more interesting test cases, for a given runtime context. We simplify this problem as finding an optimal probability distribution of mutation operators, following which the scheduler chooses next operators when testing a target program. We could first let each operator explore its own optimal probability(local). Then, based on those optimal probabilities, we could obtain a global optimal probability distribution of mutation operators.

- MOPT Main Framework--> consists of four core modules
	- the PSO initialization
    - updating modules
    - the pilot fuzzing
    - core fuzzing modules