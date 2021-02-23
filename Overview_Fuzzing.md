# Overview

- **Fuzzing** is a dynamic analysis technique which detects vulnerabilities(crashes, memory leak, unhandled exception) by testing a program with different abnormal or random inputs.

- For **generating inputs** there are some methods; for example, we can simply use the random generator files in Linux or we could simply write manually a test case script by python to generate different inputs.

	Another way is mutation, for this purpose first we create some inputs and test our program with those, for those inputs which are useful in finding bugs we could mutate them to create new inputs and test our program with the new ones.

- There are different types of **fuzzing techniques** for different purposes, therefore we need to know what are our requirements. For example, always there is a trade-off between the speed of finding bugs in a program and having high code coverage, so if we need to have more coverage we should use different technique.

	Also there are some specific fuzzing which is more useful for finding bugs against some attacks such as Denial-of-service or Side-channel attack.

- As a conclusion we need to **evaluate** fuzzing techniques to know which one in the best one for our needs. There is a collection of performance metrics as below:

  - Quantity of unique bugs
  - Quality of bugs
  - Speed of finding bugs
  - Stability of finding bugs
  - Coverage
  - Overhead.

    As an example by considering one of the metrics, speed of finding bugs, Hybrid Fuzzing can be mentioned which could find known vulnerabilities more than three times faster than Syzkaller technique.

- Another important aspect that we should consider is that, adversary like trusted parties also could do the fuzzing tests in order to find the bugs, so we should find the way to avoid this problem.

	**FUZZIFICATION** is one of the way to address this issue. In this method, developer compiles the program code in two different versions. One is compiled normally to generate a normal binary. Another one is compiled with Fuzzification techniques to generate a protected binary. Then developer distributes the protected binary version to adversary and trusted parties; so it is obvious that they cannot find many bugs quickly.
    
	On the other hand developers distribute the normal binary to trusted parties so they can do the fuzzing test on the normal binary with the native speed and find more bugs.
    
	This approach helps developer to receive bug reports from trusted parties and fix them before attackers abuse it.


