# Network Protocol Fuzzers

## Finding Security Vulnerabilities in Network Protocol Implementations
<https://wcventure.github.io/FuzzingPaper/Paper/Arxiv20_Protocols.pdf>

Symbolic execution engine explores possible paths of the protocol program using two approaches:

- Based on path exploration: when a branch is found, a symbolic executor explores each branch separately, thereby making a copy of the current state.
- Based on bounded model checking(BMC): BMC evaluates both branch sides and merges states after that branch.

##### FuSeBMC for detecting security vulnerabilities
Combination of fuzzing and symbolic execution technique without path explosion problem.

The main idea is to generate a set of test input packets using **fuzzing** to explore the state-space initially. These test inputs will guide the symbolic execution and BMC engines to explore the parts that fuzzing could not reach. In other words, it will legalize the scanning process and avoid problems such as code explosion. Then, use **symbolic execution** and **BMC** to achieve high-code coverage and replay them against an implementation, thereby observing potential violations of rules derived from the protocol specification.

Two main criteria:
- The ability to detect bugs
- The low verification time to find security vulnerabilities

<table>
    <thead>
        <tr>
            <th>Benchmark</th>
            <th>LOC</th>
            <th>Tool</th>
            <th>Result</th>
            <th>Vulnerability</th>
            <th>Time</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=3>FTP Server</td>
            <td rowspan=3>387</td>
            <td>**ESBMC**</td>
			<td>FALSE</td>
			<td>Buffer Overflow</td>
			<td>**<1s**</td>
        </tr>
        <tr>
            <td>KLEE</td>
			<td>TRUE</td>
			<td>Not detected</td>
			<td>2s</td>
        </tr>
        <tr>
            <td>Map2Check</td>
			<td>UNKNOWN</td>
			<td>Not detected</td>
			<td>2s</td>
        </tr>
		<tr>
            <td rowspan=4>Vulnserver</td>
            <td rowspan=4>248</td>
            <td>**ESBMC**</td>
			<td>FALSE</td>
			<td>Buffer Overflow</td>
			<td>**<1s**</td>
        </tr>
		<tr>
            <td>SPIKE</td>
			<td>Crashed</td>
			<td>Buffer Overflow</td>
			<td>8s</td>
        </tr>
        <tr>
            <td>KLEE</td>
			<td>FALSE</td>
			<td>Buffer Overflow</td>
			<td>2s</td>
        </tr>
        <tr>
            <td>Map2Check</td>
			<td>UNKNOWN</td>
			<td>Not detected</td>
			<td><1s</td>
        </tr>
    </tbody>
</table>


## FuSeBMC: A White-Box Fuzzer for Finding Security Vulnerabilities in C Programs
<https://arxiv.org/pdf/2012.11223.pdf>

## AFLNET: A Greybox Fuzzer for Network Protocols
<https://mboehme.github.io/paper/ICST20.AFLNet.pdf>

**AFLNET** is the first greybox fuzzer for protocol implementations. Unlike existing protocol fuzzers, AFLNET takes a mutational approach and uses state-feedback to guide the fuzzing process. AFLNET is seeded with a corpus of recorded message exchanges between the server and an actual client. No protocol specification or message grammars are required. AFLNET acts as a client and replays variations of the original sequence of messages sent to the server and retains those variations that were effective at increasing the coverage of the code or state space.

**Stateful Blackbox Fuzzing (SBF)**

Several SBF tools in academia:  Sulley, BooFuzz, 
and in the industry: Peach, beSTORM

These tools traverse a given protocol model, in form of a finite state machine or a graph, and leverage data models/grammars of messages
accepted at the states to generate (syntactically valid) message sequences and stress test the SUT. However, their effectiveness heavily depends on the completeness of the given state model and data model which are normally written manually based on the developers' understanding of the protocol specification and the sample captured network traffic between the client and the server.

**AFLNET– the first stateful CGF (SCGF) tool**

Introduced to address the aforementioned limitations of current CGF and SBF approaches.

- Fuzzing helps to generate new message sequences to cover new states and make the state model gradually more complete.
- Meanwhile, the dynamically constructed state model helps to drive the fuzzing towards more important code parts by using both the state coverage and code coverage information of the retained message sequences.

