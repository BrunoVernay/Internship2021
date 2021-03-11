# Commercial Products

## ForAllSecure Mayhem
<https://forallsecure.com/blog/top-3-technical-barriers-to-fuzzing>
<https://forallsecure.com/blog/demystifying-a-docker-image>
<https://go.forallsecure.com/hubfs/Content/Solution-Briefs/br-mayhem-for-api-solution-brief.pdf>
<https://go.forallsecure.com/hubfs/Content/Solution-Briefs/br-mayhem-solution-brief.pdf?hsLang=en>

Advanced fuzzing technique integrating symbolic execution and guided fuzzer; it also conducts regression and component testing, and fits directly into the DevOps workflow. 

Advantages:

- Fuzz testing that uncovers deep defects.
- Actionable results with zero-false positive rates.
- Autonomous testing at machine speed and scale.
- DevOps flexibility shift-lefts dynamic negative testing.
- Manage inherited risk from an unchecked supply chain.

Fuzzing techniques: AFL, Honggfuzz, LibFuzzer

###### Honggfuzz
<https://github.com/google/honggfuzz>
A security oriented, feedback-driven, evolutionary, easy-to-use fuzzer with interesting analysis options.

(Apache HTTPD,...)

## Stateful Blackbox Fuzzing (SBF)

Several SBF tools in academia:  Sulley, **BooFuzz**, 
and in the industry: **Peach**, **beSTORM**

### BooFuzz
<https://boofuzz.readthedocs.io/en/stable/>

Boofuzz features:

- Easy and quick data generation.
- Instrumentation – AKA failure detection.
- Target reset after failure.
- Recording of test data.
- Much easier install experience!
- Support for arbitrary communications mediums.
- Built-in support for serial fuzzing, ethernet- and IP-layer, UDP broadcast.
- Better recording of test data – consistent, thorough, clear.
- Test result CSV export.
- Extensible instrumentation/failure detection.
- Far fewer bugs.

### Peach
The Peach Fuzzer Platform uses automated generative and mutational modeling and intelligent test case generation to reveal the hidden bugs.
<https://gitlab.com/gitlab-org/security-products/protocol-fuzzer-ce>

##### **DevSecOps**
<https://about.gitlab.com/solutions/dev-sec-ops/>

- Continuous security testing capabilities
- Static Application Security Testing (SAST)
- Dynamic Application Security Testing (DAST)
- Dependency Scanning
- Container Scanning
- License Compliance
- Auto Remediation
- Secret Detection
- Fuzz Testing: Fuzzit(Coverage-guided Fuzz Testing), API Fuzz Testing/Peach(Behavioral Fuzz Testing)
	<https://www.youtube.com/c/GitLabUnfiltered/search?query=fuzz>

### **beSTORM**
<https://beyondsecurity.com/fuzzer-bestorm-whitepaper-2.html?cn-reloaded=1>

It is equipped with prioritization algorithms to enable complete coverage of all inputs that are likely to 'trigger' a security hole, all within a reasonable time frame.

Discover code weaknesses and certify the security strength of any product without access to source code. Test any protocol or hardware with beSTORM, even those used in IoT, process control, automotive and aerospace.

The beSTORM modules support both non-interactive protocols (such as HTTP, possibly the most common protocol in any Internet environment; used by web servers, communication products, and many others), and interactive protocols such as SMTP (used by mail servers, content filtering devices and anti-virus gateways).

beSTORM is expected to find the majority of vulnerabilities that a manual test would reveal within the first 24 hours of automated testing. The full test is expected to take several days to several months – depending on the size and complexity of the application. Distributed capabilities enable to shorten this time considerably by sharing the task between multiple machines. In any event, the testing is completely automated and requires no manual intervention.

## AFLNet: A Greybox Fuzzer for Network Protocols(stateful Coverage-based Greybox Fuzzing)
<https://github.com/aflnet/aflnet>

**AFLNet** is a greybox fuzzer for protocol implementations. Unlike existing protocol fuzzers, it takes a mutational approach and uses state-feedback, in addition to code-coverage feedback, to guide the fuzzing process. AFLNet is seeded with a corpus of recorded message exchanges between the server and an actual client. No protocol specification or message grammars are required. It acts as a client and replays variations of the original sequence of messages sent to the server and retains those variations that were effective at increasing the coverage of the code or state space. To identify the server states that are exercised by a message sequence, AFLNet uses the server’s response codes. From this feedback, AFLNet identifies progressive regions in the state space, and systematically steers towards such regions.

## APIFuzzer — HTTP API Testing Framework
<https://pypi.org/project/APIFuzzer/>

**APIFuzzer** reads your API description and step by step fuzzes the fields to validate if you application can cope with the fuzzed parameters. Does not require coding.

APIFuzzer main **features**:

- Parse API definition from local file or remote URL
- JSON and YAML file format support
- All HTTP methods are supported
- Fuzzing of request body, query string, path parameter and request header are supported
- Support CI integration
	- Generate JUnit XML test report format
	- Send request to alternative URL
	- Support HTTP basic auth from configuration
	- Save report of failed test in JSON format into the pre-configured folder
	- Log to stdout instead of syslog
- Configurable log level

## HTTP Method Fuzzing Scan
<https://support.smartbear.com/readyapi/docs/security/scans/types/fuzzing-http.html>

The **HTTP Method Fuzzing scan** finds weaknesses in the service by generating the semi-random input through HTTP methods.

How it works:

The HTTP Method Fuzzing scan generates a multitude of requests by using HTTP methods not included in the API definition.

It uses assertions to validate each response and check if it includes any information about potential vulnerabilities.

If a response passes all assertions, PASS will be logged for that response. If any assertion fails, FAIL will be logged.

## Fuzz-testing HTTP endpoints(Artillery)
<https://artillery.io/docs/guides/plugins/plugin-fuzzer.html>

The plugin lets you use Artillery to send a lot of unexpected and weird payloads to your API endpoints. You can then monitor your backend for exceptions, errors or crashes, and improve security and reliability of your system by fixing any issues uncovered.

The payloads generated by this plugin are based on [the Big List Of Naughty Strings](https://github.com/minimaxir/big-list-of-naughty-strings/) which contains a large number of inputs that are more likely to trigger unexpected behavior in your software.

## HTTP-FUZZER
<https://github.com/tehmoon/http-fuzzer>

This project **features**:

- Burp compatible
- Easy templating with Go template package
- Multi-threaded
- Multi architecture support
- Save both templated request AND response to temporary directory every time
- Wfuzz API compatible
- Use random user agent on EACH query to cover your tracks
- Use alternative wordlist to be processed for each word in the wordlist
- Follow specified number of redirects
- Throttling feature to avoid being banned

## Wfuzz
<https://wfuzz.readthedocs.io/en/latest/>
<https://github.com/xmendez/wfuzz>

**Wfuzz** is more than a web content scanner:

- Wfuzz could help you to secure your web applications by finding and exploiting web application vulnerabilities. Wfuzz’s web application vulnerability scanner is supported by plugins.

- Wfuzz is a completely modular framework and makes it easy for even the newest of Python developers to contribute. Building plugins is simple and takes little more than a few minutes.

- Wfuzz exposes a simple language interface to the previous HTTP requests/responses performed using Wfuzz or other tools, such as Burp. This allows you to perform manual and semi-automatic tests with full context and understanding of your actions, without relying on a web application scanner underlying implementation.

## SoapUI
<https://www.soapui.org/learn/security/security-vulnerability-testing/#_ga=2.84391961.16581309.1615304739-191207751.1615304739>

It is a software testing tool but not just by fuzzing technique.