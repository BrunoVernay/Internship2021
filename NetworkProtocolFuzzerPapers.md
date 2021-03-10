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


<style type="text/css">
</style>
<table class="tg">
<caption>Effectiveness. Mean coverage increase (%Increase), effect size (Aˆ12), and statistical significance (p-value) when comparing AFLNET to BOOFUZZ and AFLNWE, respectively. A Vargha-Delaney Aˆ12 measure above 0.71 indicates a large effect size in favor of AFLNET. Statistical significance is computed using the Mann-Whitney U test.</caption>
<thead>
  <tr>
    <th class="tg-c3ow"></th>
    <th class="tg-0pky">Protocol</th>
    <th class="tg-0pky" colspan="3">Branch Coverage</th>
    <th class="tg-0pky" colspan="3">Statement Coverage</th>
    <th class="tg-0pky" colspan="3">State Coverage</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow" colspan="2"></td>
    <td class="tg-0pky">%Increase</td>
    <td class="tg-0pky">A<sub>12</sub></td>
    <td class="tg-0pky">p-value</td>
    <td class="tg-0pky">%Increase</td>
    <td class="tg-0pky">A<sub>12</sub></td>
    <td class="tg-0pky">p-value</td>
    <td class="tg-0pky">%Increase</td>
    <td class="tg-0pky">A<sub>12</sub></td>
    <td class="tg-0pky">p-value</td>
  </tr>
  <tr>
    <td class="tg-c3ow" rowspan="2">AFL<sub>NET</sub> vs AFL<sub>NWE</sub></td>
    <td class="tg-0pky">FTP</td>
    <td class="tg-0pky">121.06%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">&lt;0.001</td>
    <td class="tg-0pky">79.45%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">&lt;0.001</td>
    <td class="tg-0pky">85.00%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">&lt;0.001</td>
  </tr>
  <tr>
    <td class="tg-0pky">RTSP</td>
    <td class="tg-0pky">3.49%</td>
    <td class="tg-0pky">0.335</td>
    <td class="tg-0pky">0.076</td>
    <td class="tg-0pky">2.44%</td>
    <td class="tg-0pky">0.228</td>
    <td class="tg-0pky">0.003</td>
    <td class="tg-0pky">8.58%</td>
    <td class="tg-0pky">0.392</td>
    <td class="tg-0pky">0.230</td>
  </tr>
  <tr>
    <td class="tg-c3ow" rowspan="2">AFL<sub>NET</sub> vs BOOFUZZ</td>
    <td class="tg-0pky">FTP</td>
    <td class="tg-0pky">57.73%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.026</td>
    <td class="tg-0pky">49.72%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.026</td>
    <td class="tg-0pky">37.00%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.020</td>
  </tr>
  <tr>
    <td class="tg-0pky">RTSP</td>
    <td class="tg-0pky">64.13%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.026</td>
    <td class="tg-0pky">62.09%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.026</td>
    <td class="tg-0pky">100.00%</td>
    <td class="tg-0pky">1.000</td>
    <td class="tg-0pky">0.019</td>
  </tr>
</tbody>
</table>

<table>
<caption>Bugs found and average time to error comparison</caption>
    <thead>
        <tr>
            <th></th>
            <th colspan=3>Time to Error</th>
        </tr>
        <tr>
            <th>Bug ID</th>
            <th>BOOFUZZ</th>
			<th>AFL<sub>NWE</sub></th>
			<th>AFL<sub>NET</sub></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>CVE-2018-4013</td>
            <td>>24h</td>
            <td>1h 21m 37s</td>
			<td>1h 18m 10s</td>
        </tr>
        <tr>
            <td>CVE-2019-7733</td>
            <td>>24h</td>
            <td>2h 29m 36s</td>
			<td>1h 45m 42s</td>
        </tr>
        <tr>
            <td>CVE-2019-7314</td>
            <td>>24h</td>
            <td>>24h 00m 00s</td>
			<td>1h 38m 16s</td>
        </tr>
		<tr>
            <td>CVE-2019-15232</td>
            <td>>24h</td>
            <td>0h 34m 21s</td>
			<td>0h 21m 26s</td>
        </tr>
    </tbody>
</table>

Github: <https://github.com/aflnet/aflnet>