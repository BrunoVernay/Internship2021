
Mutillidae: open source web application

<https://github.com/fuzzdb-project/fuzzdb>

sql injection

<https://portswigger.net/burp>

burp suite :We designed Burp Suite Enterprise Edition to support organizations, enabling automated scanning across their entire portfolios
(like wireshark)

Radamsa : Radamsa is an open-source fuzzing tool that can generate test-cases based on user-specified input data.


The CERT Basic Fuzzing Framework (BFF) is a software testing tool that finds defects in applications that run on the Linux and Mac OS X platforms. BFF performs mutational fuzzing on software that consumes file input.



<https://www.youtube.com/watch?v=v_eNiKvzR7s&ab_channel=Codenomicon%2CLtd>
<https://www.youtube.com/c/TheCyberMentor/search?query=fuzz>

*********************      

<https://www.youtube.com/c/GynvaelEN/search?query=fuzz>

- Channel
-----------------------------------

<https://www.youtube.com/watch?v=ysZ9w3PcYVU&ab_channel=media.ccc.de>

High speed binary fuzzing::

Fuzzing binary--> hard
Fuzzing binary in kernel --> harder

Rewriting binaries:
- Approach 0: black box fuzzing
- Approach 1: rewrite dynamically
	- Translate target at runtime
	- Terrible performance(10-100x slower)
- Approach 2: rewrite statically
	- more complex analysis
	- but much better performance
	
	
	
---------------------------------------------

For fuzzing no needs to have source code!!! how we can write the test case?!

in order to be effective fuzzer should be efficient in running test cases in terms of input choice and speed

----------------------------------------
<https://www.youtube.com/watch?v=xgfhSzAVm2s&ab_channel=OWASPNZChapter>

--------------------------------

<https://www.youtube.com/watch?v=W0ZRZyljKjo&ab_channel=FuzzingLabs-PatrickVentuzelo>

Practical python 

<https://www.youtube.com/watch?v=W0ZRZyljKjo&ab_channel=FuzzingLabs-PatrickVentuzelo>

Cargo fuzzing

--------

<https://www.youtube.com/watch?v=S8JvzWDnjc0&ab_channel=BlackHat>

Coverage-guided::: structured fuzzing
They delete expression from javascript programs instead of just changing bits(mutant--> unstructure fuzzing)

Structure fuzzing--> help you find more bugs
				--> allows you to fuzz code that doesn't accept an array of bytes

lib fuzzer ----> a coverage guided fuzzer much like AFL
main fuzzer that we use in chrome and OSS fuzz

3 technique to write structure fuzzer with lib fuzzer:
- by defining a lib fuzzer custom mutator: when lib fuzzer mutating test cases will call this function to mutate test cases rather than its default mutator. so if we are fuzzing javascript instead of using the default mutator to do stupid things like bit flipping, actually lib fuzzer will call your custom mutator that can do things like you know parse .....
- *****libprotobuf-mutator ::: will handle mutation.
protobuf is just a data format like json but with pipes, so you define a schema or spec for the inputs you want libfuzzer to mutate.
then libprotobuf-mutator will create a test case based on the spec for you.
- converting to a lib custom mutator: 

---------------------------------------
Hybrid Fuzzing

<https://www.youtube.com/watch?v=uwfMnHdbMA0&ab_channel=NDSSSymposium>

------------------------

<https://www.youtube.com/watch?v=obY7YNvVWIs&ab_channel=ExplainedEasy>

1) Installing radamsa:::

        sudo apt install gcc git make wget

        git clone http://gitlab.com/akihe/radamsa.git

        cd radamsa

        make

        sudo make install

        radamsa --version

2) Generating fuzzing test cases:::
simple example: echo 'Hello, world!' | radamsa

outputs:
- Hello, world��
- ello, worl
  orl

- Hello, wo, world!

- Helo, world!

- Hello, world!

- Hello, world!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!d!

3)Using Radamsa to fuzz a comand-line application:::

    sudo apt install jq

    nano test.json

    jq . test.json

	radamsa test.json | jq

fuzz the test Json file using radamsa and then pass it to jq. this will cause jq to read the fuzzed/manipulated test case, rather than the original valid JSON data. 	
In order to more efficiently test for vulnerabilities like this, a Bash script can be used to automate the fuzzing process, including generating test cases, passing them to the target program and capturing any relevant output.

	nano jq-fuzz.sh


4) Fuzzing request to network services(use Radamsa to fuzz a network service)
- first you need to set up the web server to use for testing --> you can do this using built-in development server that comes with the php-cli package.
- 
you will also need curl in order to test your web server.

	sudo apt install php-cli curl

- create a directory to store your web server files
- create a HTML file
- now you can run your php web server(in another terminal)

	php -S localhost:8080

- then you can test he web server using curl:

		curl localhost:8080

- you can begin to fuzz test it using Radamsa
  - you need to create a sample HTTP request to use as the input data for Radamsa
  - create a file http-request.txt
  - now you can use Radamsa to submit this HTTP request to your local web server. in order to do this you will need to use Radamsa as a TCP client, which can be done by specifying an IP address and port to connect to:
  
		radamsa -o 127.0.0.1:8080 http-request.txt

outputs:::: invalid request(Unexpected EOF, Malformed HTTP request)

5) Fuzzing network client applications(use Radamsa to fuzz a network client application)

This is achieved by intercepting responses from a network service and fuzzing them before they are received by the client.

Purpose: testing web browser(client) receiving malformed HTML from a web server or testing a DNS client receiving malformed DNS responses from a DNS server

whois -> is a simple TCP-based send/receive application(port 43)

    sudo apt install whois

    whois example.com > whois.txt

in another terminal

	radamsa -o :4343 whois.txt -n inf

Radamsa will now be running in TCP server mode, and will serve a fuzzed version of whois.txt each time a connection is made to the server

	whois -h localhost:4343 example.com