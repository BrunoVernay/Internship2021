# Overview

- **Fuzzing** is a dynamic analysis technique which detects vulnerabilities(crashes, memory leak, unhandled exception) by testing a program with different abnormal or random inputs.

- Different steps of this process:
1) Identify target system
2) Identify inputs
3) Generate fuzzed data
4) Execute fuzzed data
5) Monitor system behaviour
6) Log defects

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
    
- There is a **problem** with the normal fuzzing techniques which is related to the **libraries**.  Libraries cannot run as standalone programs, but instead are invoked through another application, so it is needed to have a special fuzzer to have a more complete code coverage called FuzzGen which is automatically synthesizing fuzzers for complex libraries in a given environment.


#### TYPES OF FUZZERS

• **_Mutation-Based Fuzzers_** alter existing data samples to create new test data.

• **_Random fuzzers_** send **random** inputs to an application. There is no systematic method to the generation of these test cases, and they do not resemble a valid input.

• **_Template fuzzers_** utilize **manually** supplied custom inputs and modify them to include anomalies. They are more effective than random fuzzers, because they resemble valid inputs.

• **_Generational fuzzers_** understand the **inner workings of its input type**. These tests are written to resemble a valid input, while evading common error-detection techniques. It is about generating the inputs from the **scratch** based on the specification/format.

• **_Protocol-based fuzzers_** are a common example of generational fuzzers.

• **_Guided fuzzers_** are intelligent, containing the capability to **monitor** and leverage the target’s behavior to **autonomously** generate new, custom test cases on-the-fly. 


##### **Classification of different fuzzer techniques**

||Mutation-Based Fuzzers|Random fuzzers|Template fuzzers|Generational fuzzers|Guided fuzzers| 
|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|
|AFL|       *     |     *       |            |||
|HFL|            |      *      |            || * |
|coverage-guided fuzzing|		*	  |			   |            |||
|symbolic analysis|			  |			   |            | | * |
|CSEFuzz|			  |			   |            |  * | * |
|V-Fuzz|			  |			   |            || * |
|DIFFUZZ|			  |			   |    *        |||
|FuzzGen|			  |		*	   |            |||
|USBFuzz|		*	  |			   |            |||
|ParmeSan|		*	  |			   |            || * |

