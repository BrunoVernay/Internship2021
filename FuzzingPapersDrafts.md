# Fuzzing Papers Drafts

**_Fuzzing_** is a software-testing technique that detects vulnerabilities by executing target programs with a large amount of abnormal or random test cases.

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

















